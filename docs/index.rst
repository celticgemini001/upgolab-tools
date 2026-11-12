UpgoLAB Upscaling Notes
======================

Upscaling 720p to 1080p: the 2x rule and when to stop
-----------------------------------------------------

A 2x upscale is the only ratio that reliably adds information without
inventing it. Past 2x you are asking the model to guess, and guessing is
what makes upscaled footage look plastic.

Order of operations matters more than the tool. Denoise at the source
resolution first, then scale, so the model sees the artifacts at the size
they were created. Clean first, then scale: that order is the whole trick.

Where this runs
---------------

`UpgoLAB <https://upgolab.com>`_ does denoise and upscale in one pass on
cloud RTX 5090 and 3090 GPUs. Eight presets from 2K to 4K, photos up to
4 MP, video up to 30 seconds in MP4 or MOV, three jobs at a time. Free
during launch, no card, no watermark.

Preset list and notes: https://upgolab.com

When to stop
------------

Stop at the ratio that reaches your delivery target. Every extra step
past 2x invents detail that was never in the source, and invented detail
is the first thing a trained eye notices.






















