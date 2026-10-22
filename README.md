# Lower-cost WallasAPI with ToAPIs

A multi-provider router by Willen Ponce in Peru, with image and video generation branches.

Independent API recipe and provider proposal; not an upstream-endorsed integration.

[English](README.md) · [es](README_es.md)

Upstream: [wubjak/wallasapi](https://github.com/wubjak/wallasapi) · fixed SHA `8f90cf1a60b559eb8640cea88651dc1875890d68`. Attribution: **Willen Ponce**. [Upstream license](UPSTREAM-LICENSE). This standalone repository contains ToAPIs community code and original API media; it does not relicense the upstream application.

## Scope

Standalone image/video calls succeeded; image output maps to the router’s path/filename/mime_type/b64_data boundary. Native routing, fallback policy and API authorization are not integrated. An uncertain paid submission must not trigger automatic fallback.

## Demo / Examples

### gpt-image-2(VIP)

![Original API output](assets/gpt-image-2-vip-089784234d.png)

### seedance-2-fast

[![Play video](assets/seedance-2-fast-cbcb3252dd.jpg)](assets/seedance-2-fast-cbcb3252dd.mp4)

[MP4 — 4.04s](assets/seedance-2-fast-cbcb3252dd.mp4)

## Corresponding API pricing

| Model | Parameters | API price | This case |
|---|---|---|---|
| gpt-image-2(VIP) | n=1, size=1:1, resolution=1K, quality=low | $0.0019/image | $0.0019 quote; actual pending |
| seedance-2-fast | duration=4, resolution=480p, aspect_ratio=16:9, generate_audio=False | $5.285714/M tokens | $0.214568 settled; MP4 4.04s; $0.053111/s observed |

Rates queried with the generation API Key on 2026-10-22. Quotes are not settled charges. For token-metered video, $/M is the billing rate; observed $/s = this case’s settled cost / decoded MP4 duration and is not a fixed future price. gpt-image-2(VIP) low/1K starts at $0.0019/image. No comparative quality, uptime or savings benchmark is claimed.

## Run

Set `TOAPIS_API_KEY` privately; use Python 3.10+. No account access token is needed for generation.

```sh
python unified_client.py --model gpt-image-2-vip --prompt-file prompts/image.txt --max-usd .10
# Quote only. Explicit paid submission:
python unified_client.py --model gpt-image-2-vip --prompt-file prompts/image.txt --max-usd .10 --live --run-id my-reviewed-example
```

Video presets use `prompts/video.txt`; the Seedance Mini image-to-video preset also needs `--image your-first-frame.png`. Same run ID + same inputs resumes the same saved task. Never remove state to retry an uncertain POST.

[Provider contract and acceptance](integration/README.md) · [Original prompts](prompts/image.txt) · [Sanitized case records](cases.json)

[Model pricing / Try ToAPIs](https://go2v.toapis.com/1022_wa) · Campaign `1022_wa`
