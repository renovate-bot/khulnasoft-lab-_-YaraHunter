---
title: Build YaraHunter
---

# Build YaraHunter

YaraHunter is a self-contained docker-based tool. Clone the [YaraHunter repository](https://github.com/khulnasoft-lab/YaraHunter), then build:

```bash
docker build --rm=true --tag=ghcr.io/khulnasoft-lab/khulnasoft_malware_scanner_ce:2.2.0 -f Dockerfile .
```

Alternatively, you can pull the official deepfence image at `ghcr.io/khulnasoft-lab/khulnasoft_malware_scanner_ce:2.2.0`.

```bash
docker pull ghcr.io/khulnasoft-lab/khulnasoft_malware_scanner_ce:2.2.0
```
