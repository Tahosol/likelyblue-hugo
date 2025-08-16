---
title: "How to Harden Firefox on Android? And Why?"
description: "My Guide to Hardening Firefox on Android, and Why You Should Do It"
keywords: "how,harden,firefox,android"
cover: ../../images/how-to-harden-firefox-mobile/cover.jpg

date: 2025-08-09T17:59:22-04:00
lastmod: 2025-08-09T17:59:22-04:00

math: false
mermaid: false

categories:
  - Guide
tags:
  - browser
  - android
  - firefox
---
## Why?

Why would anyone harden Firefox on Android? The answer can be summarized in a few keywords: Privacy, Security, and Freedom.

First, let's talk about privacy. Mobile browsers, or specifically Android browsers, are really bad for privacy. They are almost all closed-source and have questionable data collection practices. There are a few exceptions like [Cromite](https://github.com/uazo/cromite), [Fennec F-Droid](https://f-droid.org/packages/org.mozilla.fennec_fdroid/), [Ironfox](https://gitlab.com/ironfox-oss/IronFox), [Iceraven](https://github.com/fork-maintainers/iceraven-browser), [Brave](https://brave.com/), etc. They are valid options, but there are still some issues with them in my opinion.

Security is a serious issue. Cromite and Fennec are often out of date compared to the upstream. Cromite is still stuck at 138.0.7204.184, while Chrome is at [139](https://www.forbes.com/sites/daveywinder/2025/08/06/google-chrome-139---update-now-warning-issued-for-35-billion-users/) with a bunch of security updates. Fennec is stuck at 141.0.0, while Firefox is at 141.0.3. Ironfox and Brave are generally quite good at catching up with the upstream, which usually takes about 24 to 72 hours. Iceraven is a more special case. Here's a quote from the developer of Iceraven:

> It has roughly zero security

> I built this from the then-current-ish Fenix version of Firefox. I definitely can't commit to keeping it up to date, so you will get hacked, and it's signed with whatever debug keys Gradle dug up, so you will have your passwords stolen by apps pretending to be this one. Also, it claims to have a Privacy Policy, but that's just what Mozilla told it to say. I don't have my own privacy policy because I am a suspicious individual on the Internet and the app isn't supposed to send me anything anyway. It probably does still send stuff to Mozilla though.

> Remember the Iceweasle Motto:

> If you aren't me, you probably shouldn't use this.

[source](https://github.com/fork-maintainers/iceraven-browser/releases/tag/fork-0)

It can be considered a joke from the developer, and it's also a long time ago when this quote was made. However, I still feel like it doesn't vibe with me. This is why I do not consider Iceraven at all.

The last part is freedom. I like to have total control when it comes to my software, even if that means I will break it. That is why I consider Brave a not-so-great choice. There are no extensions, no about:config, etc. Don't even get me started on the AI stuff and the crypto/ads drama. So the only choice left is Ironfox. But after a while of consideration, I still think that going with a hardened Firefox will be better because Ironfox is quite new, so I doubt how long it will live.

### TL;DR Why?

All the other choices do not fit my needs because some have security issues, and some do not offer the freedom I need (also crypto issues, aka Brave).

## How to Harden Firefox on Android

Trust me, it is not that hard.

### Requirements

- A computer
- Firefox on both Android and the computer (they do not need to be the same version)
- ADB installed on your computer ([Linux](https://www.tecmint.com/install-android-debug-bridge-linux/), [Windows](https://gist.github.com/ph33nx/9b8120e8b5fde95dd2d8bf9e28a061d3))
- Enable developer options on your phone ([guide](https://dev.to/james_robert/how-to-enable-developer-options-on-android-devices-n05))
- Enable USB debugging in Android (it is in the developer options)
- Enable remote debugging via USB in Firefox on Android (it is in settings at the bottom)

### First Step

Plug the phone into the computer. Run ADB on your computer:
```
adb devices
```

### Second Step

Open Firefox on your computer and go to about:debugging. It will look like this:
![](../../images/how-to-harden-firefox-mobile/connect.webp)

If your phone does not appear in the list, make sure you completed step one properly.

Now you can connect to your phone by clicking the connect button.

### Third Step

After connecting to your phone, you will want to open Firefox on your phone and go to about:support.

You will see this on the computer's Firefox:
![](../../images/how-to-harden-firefox-mobile/support.webp)

Click on inspect.

It will look somewhat like this with the console:
![](../../images/how-to-harden-firefox-mobile/empty.webp)

### Fourth Step

Now it is the fun part of pasting code from a stranger. You will paste this (do not click enter):

```
var user_pref = function(pref, val){

  try {
    if(typeof val == "string"){

         Services.prefs.setStringPref(pref, val);
    }
    else if(typeof val == "number"){

         Services.prefs.setIntPref(pref, val);
    }
    else if(typeof val == "boolean"){

         Services.prefs.setBoolPref(pref, val);
    }
  } catch(e){
    console.log("pref:" + pref + " val:" + val + " e:" + e);
  }
}
```
It will look like this:
![](../../images/how-to-harden-firefox-mobile/js.webp)
Now you can copy the user.js content of any flavor you want, like Arkenfox, Betterfox, etc., and paste it in the console like this:
![](../../images/how-to-harden-firefox-mobile/with-js.webp)
Now you can press enter to run the code.

It should now apply. In the settings, it will show that nothing has changed, but that is a display bug. If you use the Firefox Beta/Nightly or Fennec, you can check about:config to make sure.

### uBlock
Yes, of course, we need to talk about uBlock Origin. Firefox without uBlock is like sushi without soy sauce. You will probably want to use all the [optimized versions](https://github.com/yokoffing/filterlists#optimized-lists) for Firefox from Yokoffing. It is best not to go overkill because it can harm your battery performance.

## Credit
Kudos to [gunir](https://github.com/gunir) for the Betterfox [issue 240](https://github.com/yokoffing/Betterfox/issues/240), [ndv92](https://voz.vn/u/ndv92.790519/) from Voz for the Vietnamese guide, and [Phoenix](https://codeberg.org/celenity/Phoenix) for some extra docs about the Android Firefox scene.
