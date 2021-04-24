+++
date = "2021-04-23"
title = "A Historial Review of Destiny.GG Development and Unaffiliated Forks"
tags = ["Omniliberalism"]
+++

# Preface

Over the years both the Destiny.gg codebase and spinoffs have come into the spotlight, usually devolving into typical online debate discourse about stolen code, betrayals, licensing and incorrectly given credit. Being the current maintainer of the original codebase, and handling operations for its largest deployment I want to create a point of reference to the largest misconceptions.

# Understanding GitHub and Open Source Projects

All of the code currently running the Destiny.gg website is available on GitHub and licensed under various open source licenses. Anyone can "clone" the code and get started running their own site with something as simple as a few commands.

* Website frontend https://github.com/destinygg/website (what you see)
* Chat Box https://github.com/destinygg/chat-gui (where you spam links)
* Chat Server https://github.com/destinygg/chat (where you get spammed links from)
* Chat Bot https://github.com/destinygg/chat-bot (what bans you for posting the same link 5 times)

There is no "global" open source license, and different licenses are in use on different projects.

For example. [chat-bot](https://github.com/destinygg/chat-bot/blob/master/LICENSE.md) uses the MIT License, where the [website](https://github.com/destinygg/website/blob/master/LICENSE.md) uses a Creative Commons license.

I might be from PA, but I am not going to fake being a lawyer. Licenses should always be reviewed before cloning or forking Open Source projects.

# Who Created The Website

This one is the most common misconceptions I hear. It's also the funniest. 

While I am the current maintainer of the Destiny

    * Running and maintaining the servers
    * Securing the servers, managing DDoS protection
    * Hiring developers 
    * Listening to user feedback
    * Supporting billing and account issues

I myself do not commit code to the repos, and have committed very little in the past. This can be seen through [GitHub Insights](https://github.com/destinygg/website/graphs/contributors).

![Insight](https://i.imgur.com/57kwTRK.png)

A large percentage of the codebase has been written by the 2 founders Cene and Sztanpet. Both of these members have moved on from the project.

As of more recently in 2020 Destiny hired a part time developer [11k](https://github.com/destinygg/website/commits?author=11k) to maintain the code and introduce new features. 

As for my commits? Mostly configuration files :|

![](https://i.imgur.com/nvOsyD0.png)

# Strims

Years ago, I ran an unofficial website OverRustle. This site allowed you to watch various embedded streams while chatting in destiny.gg. I ran OverRustle for 4 years from 2014 to 2018. Due to personal constraints and lack of interest in the project I decided to spin the project down. 

![OverRustle](https://i.imgur.com/gm4ZuDS.png)

At the time, there were some users maintaining and updating the OverRustle code. To keep the project alive I transferred my ownership of all assets to strims.gg. This repo has been under their control since 4/20/2018 and can be seen at https://github.com/MemeLabs/Rustla2.

Nothing Strims/MemeLabs is affiliated with Destiny or myself.

# Whiteleaf Sites

In 2019 the first fork of the Destiny website code was launched for a content creator named [Vaush](https://vaush.gg). This project was and still is lead by a developer named WhiteNervosa. This project is a similar spinoff like Strims, but was the first to use both the chat and website as a spinoff project.

After creating this website, White has gone on to creating other sites based on the Vaush codebase. These spinoff sites use a mix of both MemeLabs and Destiny code.

![WhiteLeaf Flow](https://i.imgur.com/TwYe9dL.png)

Historically there has been drama between myself and White, but we have decided to move on beyond internet drama.

Vaush and [Whiteleaf](https://www.whitele.af/) websites are unaffiliated with Destiny and myself. These sites exist in their own bubble.

# Others

It's worth noting that there are other websites in existence using the Destiny codebase. These all function in the same general method of.

1. Clone code from GitHub 
2. Rebrand the website, upload your logo and pick a domain name
3. Configure your own PayPal for payments

# Closing Thoughts

I'm not really sure why people are copying this codebase. Parts of the website are old enough to be learning their times tables in school with the first commit made [June 3rd, 2013](https://github.com/destinygg/website/commit/0fcd5fbe5adfdab1e1392bb79924c09760eac5a4). Whatever works for a buck I guess.