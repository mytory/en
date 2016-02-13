---
title: 'How to run google chrome crashed on openSUSE 13.2(Check failed: NamespaceUtils::WriteToIdMapFile("/proc/self/gid_map", gid_))'
layout: post
categories:
  - linux
tags:
  - opensuse
---

After update openSUSE, Chrome didn't run unexpectedly. I executed `google-chrome` on command line and get a below error message:

    Check failed: NamespaceUtils::WriteToIdMapFile("/proc/self/gid_map", gid_)

It seems to be occured a problem on namespace...

You can run Chrome by execute below command on a temporary basis. Perhaps it turn off namespace sandbox:

    google-chrome %U --disable-namespace-sandbox

end.

