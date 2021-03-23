+++
date = "2012-03-13T09:49:42+01:00"
title = "ADClusterMapView - How to build a clustering framework"

+++

`ADClusterMapView` is a drop-in subclass of MKMapView that displays and animates clusters of annotations. [Romain Goyet](https://twitter.com/lck) and I created it for a transportation app that needed to display thousand of stations on a map. It's available on [GitHub](https://github.com/applidium/ADClusterMapView).

![ADClusterMapView](/adclustermapview.jpg)

Choosing the best algorithm for the task and efficiently implementing it was an interesting process that I described on [Applidium's website](https://applidium.com/en/news/too_many_pins_on_your_map/).