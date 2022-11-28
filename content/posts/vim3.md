+++
title = "My desktop died"
author = ["Manuel Argüelles"]
date = 2022-11-27T21:23:00-05:00
draft = false
+++

I don't remember the exact day that my desktop PC decided to stop working, but it did, and since then I have been using a single board computer as my daily driver, the Khadas VIM3, with an old NVME drive running Manjaro. As a PC it is usable (probably better than the Raspberry Pi) but the lack of RAM memory is very noticeable. The VIM3 is an Amlogic A311D with 4 GB of RAM.

I do believe that the future of PC would be the reduced instruction set computer (RISC), I think its counter part, the complex instruction set computer (CISC) has reached his peek and there's little to no room for improvement. The adoption and development has been quite slow, but steady, we now have the Rockchip 3588, capable of handling up to 32 GB or RAM memory, check out the Firefly ITX-3588J.

Anyways, back to my VIM3. I got it working easily, pipewire was crashing the kernel, but pulse audio seems to be working fine, wayland works fine with the latest mesa package, the panfrost team is amazing, true heroes! Having a basic nvme drives definitely improves the experience. I'd probably be happy with dual monitor and more RAM... Introducing the Khadas Edge 2, it seems to have everything, 16GB or RAM, dual display, but, limited storage options, just 64GB eMMC, if you need more, i'd have to be an external drive over USB3.

Back to the Fireflyx ITX-3588J, its problem is the price, that range is similar to a modern x86 computer, hopefully as time goes by, we will see more and more RK3588 boards, maybe one with 16/32GB, dual display and nvme, in the mean time, I'd probably get back to CISC.

{{< figure src="/ox-hugo/vim3.png" >}}
