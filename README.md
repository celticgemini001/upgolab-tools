# UpgoLAB

Free AI upscaler for photos and short video, running in the browser. No install, no GPU, no account required.

**Website: [upgolab.com](https://upgolab.com)**

## What it does

Enlarges photos and short clips to 2K/4K using AI models that reconstruct detail instead of interpolating. Built for the case where the source is already damaged — compressed by a messaging app, shot indoors at high ISO, or an old scan.

| Input | Limits |
|---|---|
| Photos | up to 4 MP, JPG / PNG / WebP |
| Video | MP4 / MOV, H.264 or HEVC, up to 30 seconds per file |
| Concurrency | 3 simultaneous jobs |
| Storage | files deleted after 1 hour (guest) or 24 hours (account) |

Hardware: cloud GPU (RTX 5090 / 3090). Nothing runs on your machine.

## Eight content modes

The presets exist because different content degrades differently and needs opposite treatment.

| Mode | Use for |
|---|---|
| Natural | general photos, no visible processing |
| True Texture | skin, fabric, surfaces — preserves grain and pores |
| Ultra Crisp | text, screenshots, product shots on white |
| Denoise | compressed sources: block artifacts, dark-area noise |
| Portrait | faces, keeps hair edges intact |
| 2D Animation | line art, anime — flat fills, hard edges |
| Cinematic | film stills, shallow depth of field |
| Sharp Reality | documentary, mixed detail density |

## The order that matters

Most guides say enlarge first. That makes the model learn the compression blocks and enlarge them too. The sequence that holds up:

1. Denoise, targeting block artifacts rather than sensor grain
2. Enlarge at most 2x per axis
3. Inspect at 100% on the hair edge, not at fit-to-window
4. Grade last

### Why 2x is the ceiling

Past roughly 2x the model switches from reconstructing to inventing. Faces go waxy and small text becomes strokes that look like letters but are not. A 540p source at 2x lands at 1080p, which is enough for anything watched on a screen.

Marketing numbers describe output resolution, not recovered information.

### What is not recoverable

Out-of-focus footage is gone. The sensor never recorded that detail, and no model can know what it would have been. Motion blur from a whip pan is nearly as lost.

Test before starting: hold the original at 100%. If there is edge structure, it can probably be sharpened. If there is none, save the time.

### Compression noise is not grain

Compression imposes a regular block grid. Sensor grain is random. A generic denoiser treats the grid as noise and leaves it in place, then the upscaler amplifies it. This distinction changed results more than any model choice.

## Splitting clips over 30 seconds

Cut at keyframes so the source is not re-encoded:

```bash
ffmpeg -ss 00:01:12 -to 00:01:38 -i input.mp4 -c copy segment.mp4
```

Batch split:

```bash
ffmpeg -i input.mp4 -c copy -f segment -segment_time 30 -reset_timestamps 1 seg-%03d.mp4
```

Join without a second encode:

```bash
printf "file '%s'\n" seg-*.mp4 > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

## Comparison

| | UpgoLAB | Upscayl | Video2X | Topaz Video AI |
|---|---|---|---|---|
| Runs in browser | yes | no (desktop) | no (desktop) | no (desktop) |
| Needs a GPU locally | no | yes | yes | yes |
| Free tier | yes, unlimited during launch | yes (open source) | yes (open source) | no |
| Video support | yes, up to 30 s | no | yes | yes |
| Content-specific presets | 8 | several models | no | some |
| Watermark on free | no | no | no | n/a |

UpgoLAB trades long-clip support for zero setup. If you need a 40-minute file and have a GPU, Video2X is the better tool. If you have a phone photo and no GPU, this is.

## Limitations, stated plainly

- 30 second cap on video is a real constraint, not a marketing choice
- Photos are capped at 4 MP input
- No batch API
- Free during launch; pricing not yet announced
- Built and operated from Vietnam

## Links

- Website: [upgolab.com](https://upgolab.com)
- Notes on the denoise-then-enlarge order: [celticgemini001.github.io/upgolab-tools](https://celticgemini001.github.io/upgolab-tools/)
- Technical write-up: [dev.to/celticgemini001](https://dev.to/celticgemini001/denoise-before-upscale-the-ordering-mistake-and-why-2x-is-the-ceiling-n7m)

## License

Documentation in this repository is MIT. The UpgoLAB service itself is proprietary.
