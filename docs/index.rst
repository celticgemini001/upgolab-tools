UpgoLAB Upscaling Notes
=======================

Upscaling 720p to 1080p: the 2x rule and when to stop
-----------------------------------------------------

A 2x upscale is the only ratio that reliably adds information without
inventing it. Past 2x you are asking the model to guess, and guessing is
what makes upscaled footage look plastic.

.. figure:: https://upgolab.com/media/med_792e8b64265e4a98.jpg
   :alt: Natural HD preset - denoise then 2x upscale
   :width: 100%

   Natural HD preset: denoise at source resolution, then one 2x pass.

Order of operations matters more than the tool. Denoise at the source
resolution first, then scale, so the model sees the artifacts at the size
they were created. Clean first, then scale: that order is the whole trick.

Preset comparison
-----------------

Eight presets ship with the tool. These cover most real footage:

.. figure:: https://upgolab.com/media/med_b4fd2338fa584b1d.jpg
   :alt: Ultra Crisp preset result
   :width: 100%

   Ultra Crisp preset.

.. figure:: https://upgolab.com/media/med_1344197c4c054894.jpg
   :alt: Social Denoise preset result
   :width: 100%

   Social Denoise preset.

.. figure:: https://upgolab.com/media/med_c079d08484cf4f81.jpg
   :alt: Portrait Studio preset result
   :width: 100%

   Portrait Studio preset.

.. figure:: https://upgolab.com/media/med_6766a320efdf4f16.jpg
   :alt: Anime 2D preset result
   :width: 100%

   Anime 2D preset.

Where this runs
---------------

`UpgoLAB <https://upgolab.com>`_ does denoise and upscale in one pass on
cloud RTX 5090 and 3090 GPUs. Eight presets from 2K to 4K, photos up to
4 MP, video up to 30 seconds in MP4 or MOV, three jobs at a time. Free
during launch, no card, no watermark.

.. figure:: https://upgolab.com/media/med_ac7b6755969544f3.jpg
   :alt: Cinema Vivid preset result
   :width: 100%

   Cinema Vivid: one pass, no manual masking.

Preset list and notes: https://upgolab.com

When to stop
------------

Stop at the ratio that reaches your delivery target. Every extra step
past 2x invents detail that was never in the source, and invented detail
is the first thing a trained eye notices.

.. figure:: https://upgolab.com/media/med_048d3778f940498d.jpg
   :alt: True Texture preset preserving original grain
   :width: 100%

   True Texture: keeps original grain instead of smoothing it away.
