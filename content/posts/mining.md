+++
title = "Mining on a Raspberry PI4"
date = 2021-03-27T01:32:00-05:00
tags = ["arm", "pi4", "monero"]
draft = false
+++

I have an extra Raspberry Pi4 doing basically nothing, and with the Nano R4S on its way to replace my router I'd soon have 2 Pi4 doing nothing, so until I find a purpose for them, why not get them to mine a bit! I've been a huge fan of [Monero](https://www.getmonero.org/), I like everything of it, from the name (in Esperanto, a language that I have been slowly trying to learn) to its superb privacy. Mining Monero helps with the decentralization of the network. I did a bit of research and went with a small mining pool. Small mining pools take longer to find a block, but the reward gets divided with less people.

I downloaded the mining software called xmrig, which apparently is one of the best, fired up my Raspberry Pi4 with the aarch64 version of [Raspberry OS](https://downloads.raspberrypi.org/raspios%5Farm64/images/), downloaded and compiled the [code](https://github.com/xmrig/xmrig) and started mining. That was pretty easy, however, the hash rate was a bit small, I was getting only 88 hashes per second. Usually modern CPUs should give at least 1 or 1.5 KH/s, that's more than 10 times of what I'm getting.

This version is not [overclocked](https://www.raspberrypi.org/documentation/configuration/config-txt/overclocking.md) and I noticed that [huge pages](https://www.kernel.org/doc/html/latest/admin-guide/mm/hugetlbpage.html) were not available, I have 4 GB or RAM, so huge pages would probably improve things a bit. After googling around I found that the kernel that ships with the Raspberry OS does not includes support for huge pages. Time to recompile it, I followed the 64 bits instructions on their website to [rebuild the kernel](https://www.raspberrypi.org/documentation/linux/kernel/building.md) and enabled huge pages. The relevant entries in the configuration that were changed were:

```bash
CONFIG_CGROUP_HUGETLB=y
CONFIG_SYS_SUPPORTS_HUGETLBFS=y
CONFIG_ARCH_ENABLE_HUGEPAGE_MIGRATION=y
CONFIG_HAVE_ARCH_TRANSPARENT_HUGEPAGE=y
CONFIG_TRANSPARENT_HUGEPAGE=y
CONFIG_TRANSPARENT_HUGEPAGE_ALWAYS=y
# CONFIG_TRANSPARENT_HUGEPAGE_MADVISE is not set
CONFIG_HUGETLBFS=y
CONFIG_HUGETLB_PAGE=y
```

If you use `make menuconfig` (as I did) those are the menu options that I enabled: `Memory Management options` --> `Transparent Hugepage Support`, `File systems` --> `Pseudo filesystems` --> `HugeTLB file system support` and finally `General setup` --> `Control Group support` --> `HugeTLB controller` and that was it. I also took the opportunity to overclock the CPU a bit, I don't have a powerful fan (the ICE Tower is on its way) so I just added this to `/boot/config.txt`:

```bash
over_voltage=2
arm_freq=1700
max_framebuffers=0
gpu_mem=16
```

Which basically increases a bit the CPU clock and lowers the memory used for the GPU and frame buffers. I also changed the boot setup to start without X. With all of this, there was an improvement, but I think it can be better, probably not much better, but there's still room to overclock and fine tune the huge pages configuration. But for now, it is giving around 100 hashes per second, nothing crazy but taking in consideration that it was just collecting dust, why not.

This is the current output of xmrig:

```nil
[2021-03-20 22:59:41.396]  miner    speed 10s/60s/15m 99.61 99.70 99.71 H/s max 118.2 H/s
[2021-03-20 22:59:50.125]  cpu      accepted (5798/0) diff 3391 (146 ms)
[2021-03-20 23:00:41.442]  miner    speed 10s/60s/15m 99.61 99.61 99.70 H/s max 118.2 H/s
[2021-03-20 23:00:52.844]  cpu      accepted (5799/0) diff 3391 (144 ms)
|    CPU # | AFFINITY | 10s H/s | 60s H/s | 15m H/s |
|        0 |        0 |   24.51 |   24.64 |   24.69 |
|        1 |        1 |   24.83 |   24.79 |   24.87 |
|        2 |        2 |   24.83 |   25.07 |   25.08 |
|        3 |        3 |   25.14 |   25.06 |   25.07 |
|        - |        - |   99.31 |   99.55 |   99.70 |
[2021-03-20 23:01:03.030]  miner    speed 10s/60s/15m 99.31 99.55 99.70 H/s max 118.2 H/s
```

So, is it profitable? No, probably not, even with the little power consumption of the Pi, it's probably not worth it. However, as a relative inexpensive way of supporting the project, it's great. Just avoid the big pools; to keep the network healthy it is important to have several, independent, small pools rather than a few big ones.
