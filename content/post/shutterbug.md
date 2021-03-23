+++
date = "2012-09-10T18:13:15+01:00"
title = "Shutterbug - Image downloader for Android"

+++

When doing mobile development, we often find ourselves in the need of having to load a list of images, whether they are profile pictures, video thumbnails, or document previews. On iOS, [`SDWebImage`](https://github.com/rs/SDWebImage) is one of the best libraries available for that use. It handles image caching and offers great performance.

When looking for a similar library on Android, I couldn't find one that fitted my needs. So I decided to port `SDWebImage` to Android. It's called `Shutterbug`, and it offers most of the same features as `SDWebImage`, including an LRU (Least Recently Used) cache (both disk and memory). You can fork `Shutterbug` on [GitHub](https://github.com/applidium/Shutterbug).