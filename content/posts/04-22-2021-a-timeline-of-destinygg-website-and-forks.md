+++
date = "2021-04-26"
title = "A Historical Review of Destiny.gg Development and Unaffiliated Forks"
tags = ["Streaming","Omniliberalism","OpenSource"]
+++

# Preface

I guess I wouldn't be a true Destiny orbiter without needing to release my own manifesto. Over the years both the Destiny.gg codebase and new forks have come into the spotlight, usually devolving into typical online debate discourse about stolen code, betrayals, licensing and incorrectly given credit. Being the current maintainer of the original codebase, and handling operations for its largest deployment I want to create a point of reference to the largest misconceptions.

The views expressed here are my own, and may not reflect others' involvements in related projects or Destiny himself. There is a reason this is on cake.sh, not Destiny.gg.

# Understanding GitHub and Open Source Projects

All of the code currently running the Destiny.gg website is available on [GitHub](https://github.com/destinygg) and licensed under various open source licenses such as [Creative Commons](https://github.com/destinygg/website/blob/master/LICENSE.md), [MIT](https://github.com/destinygg/destinypositions/blob/main/LICENSE), and [Apache License 2.0](https://github.com/destinygg/chat/blob/master/README.md). Anyone can "fork" the project and "clone" the code to get started running their own site in minutes.

* Website frontend https://github.com/destinygg/website (what you see)
* Chat Box https://github.com/destinygg/chat-gui (where you spam links)
* Chat Server https://github.com/destinygg/chat (where you get spammed links from)
* Chat Bot https://github.com/destinygg/chat-bot (what bans you for posting the same link 5 times)

There is no "global" open source license and different licenses are in use on different projects.

For example, chat-bot uses the [MIT](https://tldrlegal.com/license/mit-license) License, whereas the website uses a [Creative Commons](https://creativecommons.org/licenses/by-nc-nd/3.0/deed.en_US) license.

I might be from PA, but I am not going to fake being a lawyer and pretend to understand these licenses at a deep level. Licenses should always be reviewed before cloning or forking open source projects for commercial use.

# So, Who Created The Website?

This is the most common misconception I hear. For me personally, it's also the funniest. 

While I am the current maintainer of Destiny.gg, This includes the following duties:

* Running and maintaining the servers
* Securing the platform, managing DDoS protection and our content delivery network
* Hiring developers, assigning projects to developers
* Listening to user feedback
* Supporting billing and account issues
* Code review and merging into our open source GitHub repositories

I myself do not commit code to the projects, and have committed very little in the past. This can be seen through [GitHub Insights](https://github.com/destinygg/website/graphs/contributors).

![Insight](https://i.imgur.com/57kwTRK.png)

A large percentage of the codebase has been written by the 2 founders Cene and Sztanpet. Both Cene and Sztanpet are the original authors, and created most of the website still in use today. Both of these contributors have moved on from the project in recent years.

As of more recently in 2020 Destiny hired and pays a part time developer [11k](https://github.com/destinygg/website/commits?author=11k) to maintain the code and introduce new features for his website. We also  accept community changes from pull requests if the contribution is of high quality.

As for my [commits?](https://github.com/destinygg/website/commits?author=ILiedAboutCake) Accepting pull requests and the occasional configuration file tweak.

![Nopers](https://i.imgur.com/nvOsyD0.png)

# The Era of OverRustle and Strims

Years ago, I ran a website named OverRustle. This site allowed you to watch various embedded streams while chatting in destiny.gg. I ran OverRustle for 4 years from 2014 to 2018 as an independent project. Due to personal constraints and lack of interest in the project I decided to spin the project down. 

![OverRustle](https://i.imgur.com/gm4ZuDS.png)

At the time, there were some users maintaining and updating the OverRustle code. To keep the project alive I transferred my ownership of all assets to [strims.gg](https://strims.gg). This repo has been under their control since 4/20/2018. At the time of transfer, the Strims maintainers forked a copy of the [chat server](https://github.com/MemeLabs/chat) and [chat GUI](https://github.com/MemeLabs/chat-gui) to create a website completely independent of DGG. All of their code is also available on their [GitHub](https://github.com/MemeLabs).

It should also be noted that OverRustle and the Twitch chat logging OverRustleLogs website were always different independent platforms.

Nothing Strims or MemeLabs is affiliated with Destiny or myself.

# Vaush and Whiteleaf Sites

In early 2019 the first fork of the Destiny website code was launched for a content creator named [Vaush](https://vaush.gg). This project is led by a developer named WhiteNervosa. Vaush's website was the first to completely replicate the Destiny.gg environment utilizing the chat server, client, and website code.

After creating a website for Vaush, White has gone on to creating other sites based on the Vaush codebase. These spinoff sites use a mix of both MemeLabs and Destiny code.

![WhiteLeaf Flow](https://i.imgur.com/TwYe9dL.png)

Historically there has been drama between myself and White regarding the early rollout of the Vaush website. A common misconception thrown around was this conflict was started by "stolen code". As talked about in the beginning, all of the code is open source and available on GitHub.

Personally, my problem with the launch was around private communications between White and myself providing support for initial website configuration where I believed the site was being created for White, not Vaush. At this time we have settled our grievances privately and continue our works independent of each other.

After creating a website for Vaush, White has gone on to create other similar websites under the [Whiteleaf](https://www.whitele.af/) brand. These websites are unaffiliated with Destiny and myself. These sites exist independently and in my eyes, become its own incomparable platform with the original Destiny source.

# Other Forks

It's worth noting that there are other websites in existence using the Destiny codebase but I don't think they need to be covered here, as their presence online is barely known. 

Forks will come and go, many before making it to market or being short lived. Sometimes you can find 1/2 configured clones yourself with a [pro Shodan.io account](https://www.shodan.io/search?query=http.favicon.hash:101863432) before they are fully configured!

The process for creating your very own Destiny.gg goes a bit like:

1. Clone code from GitHub
2. Buy a server from [Linode](https://www.linode.com/?r=57232eb9908d0f24a8907e61106c88f475248ac7) #shameless #ad
3. Stumble through the mess of undocumented and codependent services
4. Rebrand the website, upload your logo and pick a domain name
5. Setup your PayPal with API keys and go brrrrr

# Closing Thoughts

I'm not really sure why people are copying this codebase. Parts of the website are old enough to be learning their multiplication tables in school with the first commit made [June 3rd, 2013](https://github.com/destinygg/website/commit/0fcd5fbe5adfdab1e1392bb79924c09760eac5a4). Sometimes I'm still amazed Destiny.gg still works myself.

Recently another barrier to entry with running your very own Destiny.gg has come up. Twitch has started cracking down on ad-blocking and in the process broken stream embedding. If you have watched a partnered or affiliate Twitch streamer, you know the purple screen all too well. 

![fuck2twitch](https://i.imgur.com/Nwoa3O8.png)

If you're planning on making your own website for a Twitch streamer, know that embedding creates a sub-prime experience for end users. A quick search of [RustleSearch](https://rustlesearch.dev/?text=%22purple%20screen%22&start_date=2020-04-26&end_date=2021-04-26&channel=Destinygg) finds almost 3,000 mentions complaining about purple screen on guest embeds like watching [XQC embedded on DGG](https://www.destiny.gg/bigscreen#twitch/xqcow).

This experience might be different for YouTube streamers, or Twitch streamers without a contract (not partnered or affiliated). Since Destiny has been [Departnered](https://www.youtube.com/watch?v=pue92Q0554o) in October 2020 his website will likely remain a viable solution for time to come.

Looking forward we have begun to rewrite the site using modern frameworks privately, likely to be available late 2021 :)