+++
title = "Vortex, the keyboard"
author = ["Manuel Argüelles"]
date = 2023-01-15T23:25:00-05:00
tags = ["pi4"]
draft = false
+++

The Vortex Pok3r is a 60% keyboard that I got as a gift from a friend. It's a solid keyboard but the firmware is proprietary and quite restrictive; I like to set the arrows keys to follow the vi keybindings (h,j,k,l), this is not possible with the stock firmware, besides that I also use the caps lock key as left control, this is possible, but it is always better to have full control of all the keys. This entry is describes my journey.

{{< figure src="/ox-hugo/vortex1.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>Original keyboard" >}}

My initial goal was to just install QMK firmware, after a bit of research I came across [a fork of QMK for the Pok3r](https://github.com/pok3r-custom/qmk_pok3r), with a custom tool to [flash images](https://github.com/pok3r-custom/pok3rtool/wiki). The only missing part was how to get into the chip and replace the proprietary firmware with this on. The chip is an HT32.

{{< figure src="/ox-hugo/vortex2.jpeg" caption="<span class=\"figure-number\">Figure 2: </span>chipset" >}}

Unlocking the HT32 is possible thanks to a [fork of OpenOCD](https://github.com/ChaoticEnigma/openocd-ht32) with support to this chip, in order to connect to it an adapter/device is required, the recommended one seems to be an ST-Link (JTAG/SWD interface), unfortunately I don't have such device and I don't have a use for one rather than this project, investing in such a tool for only one project didn't seem like a good idea, lucky for me, OpenOCD supports using the GPIO pins of a Raspberry as interface and I do happen to have a Raspberry 4, so I gave it a try.

```nil
interface bcm2835gpio

debug_level 2
adapter_khz 1


### those are the numbers for pi4
bcm2835gpio_peripheral_base 0xFE000000
bcm2835gpio_speed_coeffs 236181 60


## use pinout.xyz, those are pins 38 and 40
bcm2835gpio_swd_nums 20 21

## pin 12 on the PI
bcm2835gpio_srst_num 18

## dont forget pin 9 for Ground
transport select swd

## Thanks to Borislav Nikolov
```

I saw the SWD connector on the board and went with the easy route: push some jumper wires on it and give it a try, of course that didn't work, the connection was too loose and failed randomly, even after trying to solder them the problem persisted, probably because the copper plates were on the opposite side, which makes it difficult to get a good connection without removing all the switches and resolder the wires from the (other) right side, eventually I ended up doing it.

{{< figure src="/ox-hugo/vortex3.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>First try, from the wrong side" >}}

{{< figure src="/ox-hugo/vortex4.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>With pins soldered from the right side" >}}

With a good connection it was possible to flash the HT32 with the custom firmware using the forked version of OpenOCD and from there loading the custom QMK firmware with my keymap to it using pok3rtool.

There was some rust on the plate and since I got all the brown mx switches out, I decided to paint the whole plate and case black and get some gateron yellow switches (since they are super cheap and quite decent), here are some pictures of the final product. Thanks to [Charlie Waters](https://github.com/ChaoticEnigma) for making this possible.

{{< figure src="/ox-hugo/vortex5.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>Rusty plate" >}}

{{< figure src="/ox-hugo/vortex6.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>Paint job" >}}

{{< figure src="/ox-hugo/vortex7.jpeg" caption="<span class=\"figure-number\">Figure 1: </span>Final keyboard" >}}
