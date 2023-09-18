---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "NNSVS: A Neural Network-Based Singing Voice Synthesis Toolkit"
summary: "Accepted to [ICASSP 2023](https://2023.ieeeicassp.org/)"
authors:
- admin
- Reo Yoneyama
- Tomoki Toda
tags:
- SVS
- Python
- Deep Learning
- Open-Source
- ICASSP
categories: []
date: 2022-10-18T22:17:44+09:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: "https://github.com/nnsvs/nnsvs"
url_pdf: ""
url_slides: ""
url_video: "https://www.youtube.com/watch?v=u2210L3JXPo"

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

Preprint: [arXiv:2210.15987](https://arxiv.org/abs/2210.15987) (Submitted to [ICASSP 2023](https://2023.ieeeicassp.org/))


- [Updates](#updates)
- [Authors](#authors)
- [Abstract](#abstract)
- [Systems](#systems)
- [Samples](#samples)
  - [SVS](#svs)
  - [A/S](#as)
- [Mixed demo](#mixed-demo)
  - [Sample 1](#sample-1)
  - [Sample 2](#sample-2)
  - [Sample 3](#sample-3)
- [Bonus samples](#bonus-samples)
  - [Japanese](#japanese)
  - [Mandarin](#mandarin)
- [Error cases](#error-cases)
  - [Unstable pitch of DiffSinger](#unstable-pitch-of-diffsinger)
- [Acknowledgments](#acknowledgments)
- [Appendix](#appendix)
  - [Note pitch distribution](#note-pitch-distribution)
- [References](#references)

## Updates

- 2023/02/27: Added error cases to address reviewer's comments. See [Error cases](#error-cases).
- 2022/11/27: Added samples of diffusion-based acoustic models. See [Bonus samples](#bonus-samples).
- 2022/10/18: Created the demo page.

## Authors

- Ryuichi Yamamoto (LINE Corp., Nagoya University)
- Reo Yoneyama (Nagoya University)
- Tomoki Toda (Nagoya University)

## Abstract

This paper describes the design of NNSVS, an open-source software for neural network-based singing voice synthesis research. NNSVS is inspired by Sinsy, an open-source pioneer in singing voice synthesis research, and provides many additional features such as multi-stream models, autoregressive fundamental frequency models, and neural vocoders. Furthermore, NNSVS provides extensive documentation and numerous scripts to build complete singing voice synthesis systems. Experimental results demonstrate that our best system significantly outperforms our reproduction of Sinsy and other baseline systems. The toolkit is available at https://github.com/nnsvs/nnsvs.

## Systems

The following table summarizes the systems used in our experiments. All the models were trained on Namine Ritsu's database [1].

| System                      | Acoustic Features  | Multi-stream Architecture | Autoregressive streams | Vocoder     |
|-----------------------------|--------------------|---------------------------|------------------------|-------------|
| Sinsy [2]                   | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN  [5]   |
| Sinsy (w/ pitch correction) | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN   |
| Sinsy (w/ vibrato modeling) | MGC, LF0, VUV, BAP | No                        | -                      | hn-uSFGAN   |
| Muskits RNN [3]             | MEL                | No                        | -                      | HiFi-GAN [6]   |
| DiffSinger [4]              | MEL, LF0, VUV      | Yes                       | -                      | hn-HiFi-GAN |
| NNSVS-Mel v1                | MEL, LF0, VUV      | Yes                       | -                      | hn-uSFGAN   |
| NNSVS-Mel v2                | MEL, LF0, VUV      | Yes                       | LF0                    | hn-uSFGAN   |
| NNSVS-Mel v3                | MEL, LF0, VUV      | Yes                       | MEL, LF0               | hn-uSFGAN   |
| NNSVS-WORLD v0 [1]          | MGC, LF0, VUV, BAP | No                        | -                      | WORLD       |
| NNSVS-WORLD v1              | MGC, LF0, VUV, BAP | Yes                       | -                      | hn-uSFGAN   |
| NNSVS-WORLD v2              | MGC, LF0, VUV, BAP | Yes                       | LF0                    | hn-uSFGAN   |
| NNSVS-WORLD v3              | MGC, LF0, VUV, BAP | Yes                       | MGC, LF0               | hn-uSFGAN   |
| NNSVS-WORLD v4              | MGC, LF0, VUV, BAP | Yes                       | MGC, LF0, BAP          | hn-uSFGAN   |
| hn-HiFI-GAN (A/S)           | MEL, LF0, VUV      | -                         | -                      | hn-HiFi-GAN |
| hn-uSFGAN-Mel (A/S)         | MEL, LF0, VUV      | -                         | -                      | hn-uSFGAN   |
| hn-uSFGAN-WORLD (A/S)       | MGC, LF0, VUV, BAP | -                         | -                      | hn-uSFGAN   |

Notes on baselines

- Muskits and DiffSinger baseline systems were trained with thier offical code ([Muskits](https://github.com/SJTMusicTeam/Muskits/tree/1f1855d914d2077f33ad9675866f474005cd8034/egs/namine_ritsu_utagoe_db/svs1) and [DiffSinger](https://github.com/MoonInTheRiver/DiffSinger)).
- hn-HiFi-GAN is the vocoder used by DiffSinger. The detail of its implementation can be found [here](https://github.com/nnsvs/ParallelWaveGAN/blob/5a1e0e0c6972cfa0efcbd17d4b42c453e611234d/parallel_wavegan/models/hnhifigan.py#L173).
- Sinsy systems are based on NNSVS's implementation.
- NNSVS-WORLD v0 uses the model trained with the earlier version of NNSVS (as of Nov. 2021) [1]. See [here](https://www.youtube.com/watch?v=pKeo9IE_L1I) for details.

Notes on NNSVS systems

- The code for reproducing experiments are available [here](https://github.com/nnsvs/nnsvs/tree/master/recipes/namine_ritsu_utagoe_db/icassp2023-24k-world).

## Samples

The following samples are vocal only. Mixed demo can be found [here](#mixed-demo).

### SVS

Samples generated from musical score.

<p>Sample 1: 1st color</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test01]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 2: ARROW</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test02]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 3: BC</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test03]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 4: Close to you</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test04]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Sample 5: ERROR</p>
<table><thead>
<tr><th>Recording</th><th>Sinsy</th><th>Sinsy (with pitch correction)</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy (with pitch correction).wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>Sinsy (with vibrato modeling)</th><th>Muskits RNN</th><th>DiffSinger</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Sinsy (with vibrato modeling).wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Muskits RNN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-DiffSinger.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-Mel v1</th><th>NNSVS-Mel v2</th><th>NNSVS-Mel v3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v2.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-Mel v3.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v0</th><th>NNSVS-WORLD v1</th><th>NNSVS-WORLD v2</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v3</th><th>NNSVS-WORLD v4</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-NNSVS-WORLD v4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>

### A/S

Samples generated from extracted features (i.e., analysis-by-synthesis).

<p>Sample 1: 1st color</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test01]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 2: ARROW</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test02]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 3: BC</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test03]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 4: Close to you</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test04]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 5: ERROR</p>
<table><thead>
<tr><th>Recording</th><th>hn-HiFi-GAN</th><th>hn-USFGAN-Mel</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-HiFi-GAN.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-USFGAN-Mel.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>hn-USFGAN-WORLD</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202210_nnsvs/AnaSyn/[Test05]-hn-USFGAN-WORLD.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table>

## Mixed demo

System: NNSVS-WORLD v4

### Sample 1

ERROR (from test data)

{{< youtube u2210L3JXPo >}}

### Sample 2

ARROW (from test data)

{{< youtube OqwVNUjzgAE >}}

### Sample 3

WAVE (from training data)

{{< youtube _5T0HPfeGjs >}}

## Bonus samples

We integrated the diffusion model for SVS [4] to improve naturalness of synthetic voice.
The following table summarizes the systems for bonus samples.

| System          | Acoustic Features  | Autoregressive streams | Diffusion streams | Vocoder      |
|-----------------|--------------------|------------------------|-------------------|--------------|
| NNSVS-WORLD v4* | MGC, LF0, VUV, BAP | LF0, MGC, BAP          | -                 | SiFi-GAN [7] |
| NNSVS-Mel v5    | MEL, lF0, VUV      | LF0                    | MEL               | SiFi-GAN     |
| NNSVS-WORLD v5  | MGC, LF0, VUV, BAP | LF0                    | MGC, BAP          | SiFi-GAN     |

NNSVS-WORLD v4* is the best model (as of 2022/09) reported in our paper with the following two changes:
- sampling rate was changed from 24 kHz to 48 kHz
- the vocoder was changed from hn-uSFGAN to SiFI-GAN [7].

NNSVS-Mel v5 and NNSVS-WORLD v5 are the systems using diffusion-based multi-stream acoustic models.

Note that we used 48 kHz sampling rate for the additional experiments.

### Japanese

<p>Sample 1: 1st color</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-WORLD v4*</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test01]-NNSVS-WORLD v4*.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test01]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test01]-NNSVS-WORLD v5.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 2: ARROW</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-WORLD v4*</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test02]-NNSVS-WORLD v4*.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test02]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test02]-NNSVS-WORLD v5.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 3: BC</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-WORLD v4*</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test03]-NNSVS-WORLD v4*.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test03]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test03]-NNSVS-WORLD v5.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 4: Close to you</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-WORLD v4*</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test04]-NNSVS-WORLD v4*.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test04]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test04]-NNSVS-WORLD v5.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Sample 5: ERROR</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-WORLD v4*</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test05]-NNSVS-WORLD v4*.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test05]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>NNSVS-WORLD v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS/[Test05]-NNSVS-WORLD v5.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table>



### Mandarin

We provide Mandarin SVS samples using [Opencpop database](https://wenet.org.cn/opencpop/) [8].

<p>Sample 1: 2044001628</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test01]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test01]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Sample 2: 2044001629</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test02]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test02]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Sample 3: 2092003412</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test03]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test03]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Sample 4: 2093003457</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test04]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test04]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Sample 5: 2093003458</p>
<table><thead>
<tr><th>Recording</th><th>NNSVS-Mel v5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test05]-Recording.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202211_nnsvs/SVS_opencpop/[Test05]-NNSVS-Mel v5.wav" type="audio/wav"></audio></td>
</tr></tbody></table>

## Error cases

### Unstable pitch of DiffSinger

<div align="center"><img src="/images/nnsvs/error_diffsinger_unstable_pitch.png" width="100%" /></div>

<table><thead>
<tr><th>DiffSinger</th><th>Recording</th></tr>
</thead>
<tbody>
<tr>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-DiffSinger.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/202210_nnsvs/SVS/[Test05]-Recording.wav" type="audio/wav"></audio></td>
</tr></tbody></table>

As shown in the figure (blue: discontinous F0; green: unstable vibrato), the pitch contour of the DiffSinger is sometimes unstable.

## Acknowledgments

This work was partly supported by JST CREST Grant Number JPMJCR19A3.

## Appendix

### Note pitch distribution

We selected test songs to cover a wide range of note pitches. Their distributions are shown in the following figure.

<div align="center"><img src="/images/ritsu_pitch_dist.png" width="100%" /></div>

Pitch is presented as MIDI note number, where A4 (69) corresponds to 440 Hz.
The lowerest and highest notes of the test songs were D#4 (155.6 Hz) and A5 (880 Hz), whereas those of the training data were D#3 (146.8 Hz) and B5 (987.8 Hz).

## References

- [1] Canon, [NamineRitsu] Blue (YOASOBI) [ENUNU model Ver.2, Singing DBVer.2 release], https://www.youtube.com/watch?v=pKeo9IE_L1I, Accessed: 2022.10.06.
- [2] Y. Hono, K. Hashimoto, K. Oura, et al., “Sinsy: A deep neural network-based singing voice synthesis system,” IEEE/ACM Trans. on Audio, Speech, and Language Processing, vol. 29, pp. 2803.
- [3] J. Shi, S. Guo, T. Qian, et al., “Muskits: an End-to-end Music Processing Toolkit for Singing Voice Synthesis,” in Proc. Interspeech, 2022, pp. 4277–4281.
- [4] J. Liu, C. Li, Y. Ren, et al., “DiffSinger: Singing Voice Synthesis via Shallow Diffusion Mechanism”, AAAI, vol. 36, no. 10, pp. 11020-11028, Jun. 2022.
- [5] R. Yoneyama, Y.-C. Wu, and T. Toda, “Unified Source-Filter GAN with Harmonic-plus-Noise Source Excitation Generation,” in Proc. Interspeech, 2022, pp. 848–852.
- [6] J. Kong, J. Kim, and J. Bae, “HiFi-GAN: Generative adversarial networks for efficient and high fidelity speech synthesis,” NeurIPS, vol. 33, pp. 17 022–17 033, 2020.
- [7] R. Yoneyama, Y.-C. Wu, and T. Toda, “Source-Filter HiFi-GAN: Fast and Pitch Controllable High-Fidelity Neural Vocoder." arXiv preprint arXiv:2210.15533, 2022.
- [8] Y. Wang, X. Wang, P. Zhu, et al., “Opencpop: a high-quality open source chinese popular song corpus for singing voice synthesis," arXiv:2201.07429, 2022.
