---
layout: post
title: "esoTalk Arabic Support"
image: uploads/esotalk-screenshot.png
---

I've been asked at the company to use/implement forum software with simple/clean theme and footprint.

After a little search I found [esoTalk](http://esotalk.org), a very nice *fat free* forum.

To have Arabic support in esoTalk you've to implement 2 things; RTL Skin (theme) and Arabic language pack.

## RTL Skin

Default esoTalk skin is very nice and clean, here's my Default RTL skin, it looks the same as Default skin but with RTL support and **Droid Arabic Kufi** web font.

### Installation

- Download the [zip file](https://github.com/AAlakkad/esoTalk-DefaultRTL-skin/archive/master.zip) and extract its content in `addons/skins`.
- Rename the extracted folder to `DefaultRTL`.
- Then go to `Appearance` in administration panel and activate the skin.

### Admin Skin

The skin by default will be used for front-end only, you can use this skin for admin panel by adding this line to your `config/config.php` file:

```php
$config["esoTalk.adminSkin"] = 'DefaultRTL';
```

## Arabic Language Pack

The language pack isn't complete yet, but you can use it (and help me finish it if you want!).

### Installation

- Download the [zip file](https://github.com/AAlakkad/esoTalk-Arabic-Translation/archive/master.zip) and extract its content in `addons/language/Arabic`.
- Rename the extracted folder to `Arabic`.
- Then go to `Settings` in administration panel and activate the language.


## Contribution

You're welcome to [report a bug](https://github.com/AAlakkad/esoTalk-DefaultRTL-skin/issues) in RTL theme, or [suggestion/update](https://github.com/AAlakkad/esoTalk-Arabic-Translation/issues) translation.
