+++
date = "2020-10-13"
title = "Multistreaming RTMP in the Cloud using OBS, Nginx, and Docker"
tags = ["Twitch","YouTube","Streaming","AWS","Docker"]
+++

### First I not your Lawyer, OK?

A very important caveat to consider before attempting to multistream is that the [Twitch Affiliate Agreement](https://www.twitch.tv/p/legal/affiliate-agreement/) and partnership contracts* have an exclusivity clause which multistreaming can violate.** Always read what you sign folks.

* *Some legacy contracts only apply the exclusivity deal for gaming content.
* **You can negotiate a contract with multistreaming. Your milage may vary.

### But Why?

Recently the streamer Destiny was departnered from Twitch and was free to stream again on multiple platforms. He wanted to stream to YouTube and Twitch at the same time, and we needed an elegant solution that is relatively easy to use. Some of the options we came up with was:

1. Using an existing service like restream.io
2. An [OBS Plugin](https://obsproject.com/forum/resources/multiple-rtmp-outputs-plugin.964/) to stream to multiple outputs
3. An RTMP self-hosted hosted proxy

While using restream.io was the easiest it also seemed to have the most problems. YouTube Studio did not work and at one point two YouTube streams were running in a loop. In addition, transcoding by the hour could get expensive for running daily 7-10 hour streams. Great concept, poor execution at scale.
Currently the OBS Plugin seems to be the winner for this use case as the streamer has access to a high end HEDT [2 PC streaming setup](https://www.reddit.com/r/Destiny/comments/ced38d/current_build_july_2019/), and high speed symmetric fiber optic internet. While this may work having access to a dedicated $1,900 CPU for encoding and fiber internet, most people do not have access to this. Additionally, there are still instances where utilizing this hardware is not possible such as mobile streaming or staying somewhere with limited bandwidth are which all possibilities, at least maybe again in a post-COVID world.

### A Tale of 2? Platforms

Twitch and YouTube have some major differences in how they handle the provided RTMP stream. Twitch will always offer the true source quality material but might not offer playback quality options, where YouTube will always offer quality playback options. The downside to this, is YouTube always offers a transcode, and never the source quality which can sometimes look "worse."

Twitch:
* (+) Your source quality, is the actual source
* (+) Low latency mode
* (-) 6-8mbps bitrate cap
* (-) Depending on server load and viewership you might not get quality playback options

YouTube:
* (+) You always get quality playback options
* (+) Low latency mode
* (-) 15-20mbps bitrate recommended
* (-) Your stream is always going to look worse than on Twitch


### The Restreamer + Transcoder - [atcakelabs/rtmp-nginx-docker](https://github.com/atcakelabs/rtmp-nginx-docker)

For our example lets use the the Destiny use-case where we want to stream with the following requirements; 15mbps to YouTube, and 6mbps to Twitch, both at 1080p 60fps.

![nginx-rtmp diagram](/multistreaming-in-the-cloud/multistreaming.png)

Getting started is pretty easy, the only requirements are having a system with Docker + docker-compose installed.

```Bash
git clone https://github.com/atcakelabs/rtmp-nginx-docker.git
```

Getting set up to use the proxy + transcoder is easy as updating some variables in your `docker-compose.yml`

* `PUBLISH_IP` - This should be the IP address of your streaming client, https://ipchicken.com/
* `X264_THREADS` - How many threads ffmpeg should be using, I set this to n-1 where n is total cores available.
* `X264_PRESET`- The slower, the more powerful CPU + `X264_THREADS` you need. The faster, the worse the quality. Read more on the [OBS blog](https://obsproject.com/blog/streaming-with-x264#presets).
* `TRANSCODE_BITRATE` - ffmpeg bitrate target in kbps.
* `TRANSCODE_RESOLUTION` - ffmpeg frame size target.
* `TRANSCODE_FRAMERATE` - ffmpeg fps target.
* `TWITCH_INGEST` - This should be closest region to your server. Find all regions at https://stream.twitch.tv/ingests/.
* `TWITCH_STREAMKEY` - Your Twitch streamkey.
* `YOUTUBE_STREAMKEY` - Your YouTube streamkey.

```Bash
        environment:
            - HTTP_PORT=8000
            - PUBLISH_IP=1.2.3.4
            - X264_THREADS=7
            - X264_PRESET=medium
            - TRANSCODE_BITRATE=6000k
            - TRANSCODE_RESOLUTION=1920x1080
            - TRANSCODE_FRAMERATE=60
            - TWITCH_INGEST=live-iad05
            - TWITCH_STREAMKEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
            - YOUTUBE_STREAMKEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

```

For testing you can configure both streams without going live. To do this on Twitch append `?bandwidthtest=true` to your streamkey. You will be able to see bandwidth + health of the stream at https://inspector.twitch.tv/. Or on YouTube set the stream to Unlisted or Private in YouTube Studio.

Once the environment is configured you can start the server with a single command.

```Bash
docker-compose up
```

![docker-compose up](/multistreaming-in-the-cloud/dc-up.png)

If the container has started up, open the settings menu inside OBS. In here navigate to the stream tab, click the service dropdown, and select `Custom`.
Your Server address is going to be `rtmp://$serverip:1935/live`.

![obs server setting](/multistreaming-in-the-cloud/obs.png)

No stream key is required, security of the streaming endpoint is handled by the `PUBLISH_IP` variable. Only your IP address will be able to connect and "push" an RTMP stream. Still, it is probably best to take care and not leak the IP/Name of your server :)

And then simply go live, your stream is now going to both Twitch and YouTube!

Along with running the RTMP proxy, nginx is also running a stats server. Visiting `http://$serverip:8000/stat` provides a panel to see RTMP health. **Note, this displays your streaming keys in plain text.** While this is site is again only accessible via your IP address you do not want to leak on stream, unless you want to speedrun 100% re-key all your streaming services.

![stats](/multistreaming-in-the-cloud/stat.png)

This test was completed on an Amazon EC2 Compute-Optimized Spot VM `c5n.2xlarge` averaging 25%.

![stats](/multistreaming-in-the-cloud/transcoder.png)

### The Restreamer - Source Only

Of course, not everyone wants to spend hundreds a month on a cloud server just to get 10% better quality on YouTube. If you want to send the same source stream to Twitch and YouTube without transcoding, copy the `nginx-source-only.conf` to be `nginx.conf`. When using the source only config the bandwidth set in OBS will be what goes to all providers, make sure to set an appropriate bitrate that is supported on all services.

```Bash
mv nginx-source-only.conf nginx.conf
docker-compose up
```

This method can be run on a small $10/month cloud VPS through a provider like [Linode](https://www.linode.com/?r=57232eb9908d0f24a8907e61106c88f475248ac7).

![nginx-rtmp diagram](/multistreaming-in-the-cloud/multistreaming-source.png)

### Additional Streaming Sites (Advanced)

If the provider supports sending your stream as RTMP, you can easily hook into `nginx.conf` and add additional sites and send either the transcoded stream or source stream.

The `obsproject/obs-studio` GitHub repo contains a list of RTMP servers https://github.com/obsproject/obs-studio/blob/master/plugins/rtmp-services/data/services.json included inside of OBS Studio.

But what if you wanted to send your transcoded 720p stream to Chaturbate and OnlyFans, but send the original 1080p stream to Twitch, YouTube, and DLive? This is possible by tweaking the `nginx.conf` and adding some variables to `docker-compose.yml`.

```Bash
application transcode {
    ...

    push rtmp://live.stream.highwebmedia.com/live-origin/${CHATURBATE_STREAMKEY};
    push rtmp://route0.onlyfans.com/live/${ONLYFANS_STREAMKEY};
}

application source {
    ...

    push rtmp://${TWITCH_INGEST}.twitch.tv/app/${TWITCH_STREAMKEY};
    push rtmp://a.rtmp.youtube.com/live2/${YOUTUBE_STREAMKEY};
    push rtmp://stream.dlive.tv/live/${DLIVE_STREAMKEY};
}
```

And add your streaming keys as environment variables in the `docker-compose.yml`

```Bash
environment:
    - HTTP_PORT=8000
    - PUBLISH_IP=1.2.3.4
    - X264_THREADS=2
    - X264_PRESET=fast
    - TRANSCODE_BITRATE=3000k
    - TRANSCODE_RESOLUTION=1280x720
    - TRANSCODE_FRAMERATE=30
    - TWITCH_INGEST=live-iad05
    - TWITCH_STREAMKEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    - YOUTUBE_STREAMKEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    - DLIVE_STREAMKEY=xxxxxxxxxxxxxxxxx
    - ONLYFANS_STREAMKEY=xxxxxxxxxxxxxxxxxxxx
    - CHATURBATE_STREAMKEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

With just some basic additions we are now able to stream on 5 platforms sending 6mbps in, and 24mbps out. This is just an example to demonstrate the flexibility a setup like this can provide.

![nginx-rtmp diagram](/multistreaming-in-the-cloud/multistreaming-meme.png)

### Closing Notes

Hopefully, this information saves the time of others. There are many existing nginx-rtmp Docker containers, but none configured for actually multistreaming live streams. The image itself used is [alfg/docker-nginx-rtmp](https://github.com/alfg/docker-nginx-rtmp).
