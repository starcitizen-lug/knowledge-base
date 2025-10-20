---
title: "💖 AMD"
description: "Known issues and troubleshooting steps for AMD users running Star Citizen on Linux"
parent: "Troubleshooting"
nav_order: 6
---

# 💖 AMD

## Current known issues
- See the AMD section of our [latest news](/#news)

[Add a new](/Tips-and-Tricks#how-to-edit-the-launch-script)
## Vulkan Beta: Bright flickering lights at edges of in-game display panels
- To fix: [Add environment variable](/Tips-and-Tricks#how-to-edit-the-launch-script) `radv_zero_vram=true`


## Severe frame drops
- Some Penguins see framerate or stuttering with low VRAM < 8GB
- To  fix: [Add environment variable](/Tips-and-Tricks#how-to-edit-the-launch-script) `RADV_PERFTEST=nogttspill`
