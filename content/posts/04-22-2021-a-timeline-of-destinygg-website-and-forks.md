+++
date = "2021-04-23"
title = "A Historial Review of Destiny.GG Development and Unaffiliated Forks"
tags = ["Omniliberalism"]
+++

# Preface

I guess I wouldn't be a true Destiny orbiter without needing to release my own manifesto. Over the years both the Destiny.gg codebase and spinoffs have come into the spotlight, usually devolving into typical online debate discourse about stolen code, betrayals, licensing and incorrectly given credit. Being the current maintainer of the original codebase, and handling operations for its largest deployment I want to create a point of reference to the largest misconceptions.

The views expressed here are my own, and may not reflect others involvements in related projects or Destiny himself. There is a reason this is on cake.sh, not destiny.gg.

# Understanding GitHub and Open Source Projects

All of the code currently running the Destiny.gg website is available on [GitHub](https://github.com/destinygg) and licensed under various open source licenses such as [Creative Commons](https://github.com/destinygg/website/blob/master/LICENSE.md), [MIT](https://github.com/destinygg/destinypositions/blob/main/LICENSE), and [Apache License 2.0](https://github.com/destinygg/chat/blob/master/README.md). Anyone can "fork" the project and "clone" the code to get started running their own site in minutes.

* Website frontend https://github.com/destinygg/website (what you see)
* Chat Box https://github.com/destinygg/chat-gui (where you spam links)
* Chat Server https://github.com/destinygg/chat (where you get spammed links from)
* Chat Bot https://github.com/destinygg/chat-bot (what bans you for posting the same link 5 times)

There is no "global" open source license, and different licenses are in use on different projects.

For example. [chat-bot](https://tldrlegal.com/license/mit-license) uses the MIT License, whereas the [website](https://creativecommons.org/licenses/by-nc-nd/3.0/deed.en_US) uses a Creative Commons license.

I might be from PA, but I am not going to fake being a lawyer and pretend to understand these licenses at a deep level. Licenses should always be reviewed before cloning or forking open source projects for commercial use.

# Who Created The Website

This one is the most common misconceptions I hear. To me, it's also the funniest. 

While I am the current maintainer of the Destiny, This includes the following duties:

    * Running and maintaining the servers
    * Securing the platform, managing DDoS protection and content delivery 
    * Hiring developers, assigning projects to developers
    * Listening to user feedback
    * Supporting billing and account issues

I myself do not commit code to the projects, and have committed very little in the past. This can be seen through [GitHub Insights](https://github.com/destinygg/website/graphs/contributors).

![Insight](https://i.imgur.com/57kwTRK.png)

A large percentage of the codebase has been written by the 2 founders Cene and Sztanpet. Both of these members have moved on from the project in the last few years.

As of more recently in 2020 Destiny hired and pays a part time developer [11k](https://github.com/destinygg/website/commits?author=11k) to maintain the code and introduce new features. We also routinely accept community changes from pull requests.

As for my [commits?](https://github.com/destinygg/website/commits?author=ILiedAboutCake) Mostly configuration files.

![](https://i.imgur.com/nvOsyD0.png)

# Strims

Years ago, I ran an unofficial website OverRustle. This site allowed you to watch various embedded streams while chatting in destiny.gg. I ran OverRustle for 4 years from 2014 to 2018 as an independent project. Due to personal constraints and lack of interest in the project I decided to spin the project down. 

![OverRustle](https://i.imgur.com/gm4ZuDS.png)

At the time, there were some users maintaining and updating the OverRustle code. To keep the project alive I transferred my ownership of all assets to strims.gg. This repo has been under their control since 4/20/2018 and can be seen at https://github.com/MemeLabs/Rustla2. At the time of transfer, the Strims maintainers forked a copy of the [chat server](https://github.com/MemeLabs/chat) and [chat GUI](https://github.com/MemeLabs/chat-gui) to create a website completely independent of DGG.

Nothing Strims/MemeLabs is affiliated with Destiny or myself.

# Whiteleaf Sites

In 2019 the first fork of the Destiny website code was launched for a content creator named [Vaush](https://vaush.gg). This project was and still is lead by a developer named WhiteNervosa. Vaush's website is a similar spinoff like Strims, but was the first to use both the chat and website as a spinoff project.

After creating this website, White has gone on to creating other sites based on the Vaush codebase. These spinoff sites use a mix of both MemeLabs and Destiny code.

![WhiteLeaf Flow](https://i.imgur.com/TwYe9dL.png)

Historically there has been drama between myself and White regarding the early rollout of the Vaush website. A common misconception thrown around was this conflict was started by "stolen code". As talked about above, the code is all open source on GitHub.

Personally, my problem with the launch was around private communications between White and myself providing support for initial website configuration where I believed the site was being created for White, not Vaush. At this time we have settled our grievances privately and continue our works independent of each other.

Vaush and other [Whiteleaf](https://www.whitele.af/) websites are unaffiliated with Destiny and myself. These sites exist in their own bubble.

# Other Forks

It's worth noting that there are other websites in existence using the Destiny codebase. These all function in the same general method of.

1. Clone code from GitHub 
2. Rebrand the website, upload your logo and pick a domain name
3. Configure your own PayPal for payments

# Closing Thoughts

I'm not really sure why people are copying this codebase. Parts of the website are old enough to be learning their multiplication tables in school with the first commit made [June 3rd, 2013](https://github.com/destinygg/website/commit/0fcd5fbe5adfdab1e1392bb79924c09760eac5a4). Sometimes I'm still amazed Destiny.gg still works myself.

Another barrier to entry to running your own dgg has recently come up. Within the last 3 months Twitch has started cracking down on ad-blocking and stream embeds. If you have watched a partnered or affiliate Twitch streamer, you know this screen all too well. 

![fuck2twitch](https://i.imgur.com/Nwoa3O8.png)

This change is hostile to running an embed site and provides users with a sub-prime experience. Since Destiny has been [Departnered](https://www.youtube.com/watch?v=pue92Q0554o) we continue to exist in a bubble where the purple screen doesn't impact our users.