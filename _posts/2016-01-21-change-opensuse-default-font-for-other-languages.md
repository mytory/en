---
title: Change system default font for other language in OpenSuse
layout: post
categories:
  - linux
tags:
  - opensuse
---

I have used OpenSuse during 21 months. Version is up to 13.2 in the meantime.

At the first time, I'd spent time to change default system font that render hangul ugly to ‘NanumGothic’ Korean hangul font. After than, I met a good font. It is [KoPub Font](http://www.kopus.org/biz/electronic/font.aspx). So I tried to change system font to KoPub font. But, I couldn't remember the method. OTL;;

Other method __Configure Desktop > Fonts__ menu is not good because no distinction of serif and sans-serif.

At the end of several attempts I came to know today. This method is not precise. I just fixed all things to doubt.

Go to `/etc/fonts/conf.d` folder, and open `40-nonlatin.conf`, `60-family-prefer.conf`, `65-nonlatin.conf` files. Add fonts you want by file syntax. As for me, set `KopubBatang Light` for serif, `KopubDotum Light` for sans-serif. 

Then, logout and login. Wow~! Solved system font problem fret my gizzard~!

Ah, for reference, fixed font is set by [D2Coding](http://dev.naver.com/projects/d2coding/download).