+++
title = "无聊药丸"
weight = 1
draft = false

bio = "Boredom kills!"
avatar = "images/logo.png"

[[social]]
  icon = "weixin"
  iconPack = "fab"
  url = "https://example.com/"

[[social]]
  icon = "github"
  iconPack = "fab"
  url = "https://example.com/"

[[social]]
  icon = "rss"
  iconPack = "fas"
  url = "rss/"

[widget]
  handler = "about"
    
  # Options: sm, md, lg and xl. Default is md.
  width = ""

  [widget.sidebar]
    # Options: left and right. Leave blank to hide.
    position = ""
    # Options: sm, md, lg and xl. Default is md.
    scale = ""
    
  [widget.background]
    # Options: primary, secondary, tertiary or any valid color value. Default is primary.
    color = "secondary"
    
    # See TODO
    image = ""
    # Options: auto, cover and contain. Default is auto.
    size = ""
    # Options: center, top, right, bottom, left.
    position = ""
    # Options: fixed, local, scroll.
    attachment = ""
+++

<style>
  #about > div > div + div + div{
    margin-left: 0 !important;
  }
</style>