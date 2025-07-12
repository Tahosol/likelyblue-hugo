---
title: "My Experience With Antivirus on Linux"
description: "My experience with antivirus on linux"
keywords: "my,experience,with,antivirus,on,linux"
cover: ../../images/my-experience-with-antivirus-on-linux/cover.jpg

date: 2025-06-18
lastmod: 2025-06-18

math: false
mermaid: false

categories:
  - Opinion
tags:
  - linux
  - antivirus
  - clamav
---
So I installed Anti-Virus software on my Linux system, and the reason behind it is pretty simple: I was bored. Yea! In my opinion, there is no better reason than that. I wanted to have fun tinkering with something, and AV seemed like a good idea at the time. I don't think everyone on Linux needs to have AV, and in fact, I believe it's quite useless on Linux for now. If you're interested in learning more about the subject(AV), you can visit [this blog](https://easylinuxtipsproject.blogspot.com/p/security.html#ID1.1). For me, this was just for testing and learning purposes.

My journey started with research. I stumbled upon [this blog](https://www.redhat.com/en/blog/3-antimalware-solutions) on Red Hat, read it a bit, and then decided to go with ClamAV because it seemed less sysadmin-oriented and more desktop-friendly. After making my decision, I followed the [archwiki](https://wiki.archlinux.org/title/ClamAV) to setup clamav with OnAccessScan.


> On-access scanning is the real-time protection daemon which will scan the file while reading, writing or executing it. It can be configured to either notify on detection or prevent/block on detection.

<sub>--Archwiki</sub>

There are a lot of other choices though.
Here is a list:

- [Rkhunter](https://rkhunter.sourceforge.net/) (basically obsolete)

- [Clamtk](https://gitlab.com/dave_m/clamtk/) GUI for clamav

- [Hostsblock](https://gaenserich.github.io/hostsblock/) (I think it is dead)

- [chkrootkit](https://www.chkrootkit.org/) Rkhunter but less dead

There are also more "familiar" names like Avast, Bitdefender, and Sophos, but I don't think I need to explain why I'm not considering them.

What is the benefic of using antivirus software on Linux? In short, it's non-existent. I don't feel like I'm any safer or anything at all(except the downside that I will mention later). I do test the AV software by downloading Windows malware to see how it responds. It works; I receive notifications when I start downloading malware and things like that. However, as a Linux user, I will almost certainly not be harmed by Windows malware anyway, unless I run it in Wine. Yep, Wine is so good it is [malware compatible](https://gitlab.winehq.org/wine/wine/-/wikis/FAQ#is-wine-malware-compatible).

Now, let's discuss the downsides. First of all, it's the RAM usage. To be honest, my PC has 32 GB of RAM, so it won't be a problem for me. Nevertheless, seeing my idle RAM usage double(from 1.3GB to 3.8GB) is still quite painful. By the way, ClamAV will only consume RAM like this if you run it in OnAccessScan mode. Therefore, the ClamAV scanner/ClamTK folks don't need to worry about their idle RAM. The other problem I've realized is that ClamAV's OnAccessScan feature affects system performance when you first boot up and also slightly when gaming. I've never done any formal benchmarks, so it's just an "eyeball test" so take my words with a grain of salt.

That's my experience with AV on Linux. Will I keep ClamAV on my system? Probably. Thanks for taking the time to read this rant!
