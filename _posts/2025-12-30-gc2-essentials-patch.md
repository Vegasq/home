---
layout: post
title: "Ground Control 2 Wireless Devices Fix and GC2: Essentials"
date: 2025-12-30
categories: projects gaming community-patch
---

I have always been a big fan of RTS games. And in late 90s-early 2000s there were plenty. Even outside of names like **Warcraft**, **Starcraft** or **Age of Empires**. I have lots of good memories playing **Battle Realms**, **Earth 2160** (*Where do I go? What do I do?*) and my current nostalgia trip - **Ground Control 2**. So I grabbed a copy from GOG, installed it and... Immediate crash. Oh well. Been there before.

Quick trip to [pcgamingwiki.com](https://www.pcgamingwiki.com/wiki/Ground_Control_II:_Operation_Exodus) told me to unplug all my wireless usb devices? Huh? Have you seen how hard is it to get to the back of my PC? We need a different approach.

<!--more-->

Okay, so the game is old, and used DirectX 7, and more specifically dinput, as we can deduct from the fact that unplugging wireless mouse and keyboard is an easy fix. And this thing is known to cause issues, much so some projects already exist to address issues with it. See [dinputto8](https://github.com/elishacloud/dinputto8). Sadly it did not help.

Good news is that dinput is small, and by making a simple pass-thru proxy dll that would log every call we can identify exactly who is being naughty. Aaaand, here we go. `EnumDevicesA` is the last call before the crash. Some more digging pointed me towards ancient knowledge that there are 2 magical global devices: `GUID_SysKeyboard` and `GUID_SysMouse`. And technically they are still supported... So from now on our game will only know about those 2 input devices. And after quick stop at `GetDeviceInfo` that predictably crashed, game happily launched.

Mostly done with the human campaign at this point.

And as a last push for perfection I combined it with few other patches and fixes to create a single archive that will make your experience less bumpy. Check out links below.

See ya!

[Visit GC2 Essentials](https://gc2.mkla.dev) | [View the Wireless Fix on GitHub](https://github.com/Vegasq/Ground-Control-2-wireless-fix)
