---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Description-based Controllable Text-to-Speech with Cross-Lingual Voice Control"
summary: "Submitted to ICASSP 2025"
authors:
- admin
- Yuma Shirahata
- Masaya Kawamura
- Kentaro Tachibana
tags: []
categories: []
date: 2024-09-09T21:00:18+09:00
draft: false

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

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

Submitted to [ICASSP 2025](https://2025.ieeeicassp.org/)

- [Abstract](#abstract)
- [Figure](#figure)
- [Comparison of different systems](#comparison-of-different-systems)
  - [English TTS](#english-tts)
  - [Japanese TTS](#japanese-tts)
- [Style controllability samples](#style-controllability-samples)
  - [Pitch control (en)](#pitch-control-en)
  - [Speed control (en)](#speed-control-en)
  - [Pitch control (ja)](#pitch-control-ja)
  - [Speed control (ja)](#speed-control-ja)

## Abstract

We propose a novel description-based controllable text-to-speech (TTS) method with cross-lingual control capability. To address the lack of audio-description paired data in the target language, we combine a TTS model trained on the target language with a description control model trained on another language, which maps input text descriptions to the conditional features of the TTS model. These two models share disentangled timbre and style representations based on self-supervised learning (SSL), allowing for disentangled voice control, such as controlling speaking styles while retaining the original timbre. Furthermore, because the SSL-based timbre and style representations are language-agnostic, combining the TTS and description control models while sharing the same embedding space effectively enables cross-lingual control of voice characteristics. Experiments on English and Japanese TTS demonstrate that our method achieves high naturalness and controllability for both languages, even though no Japanese audio-description pairs are used.

## Figure

<div align="center">
<figure>
  <img src="/images/nansyttspp/nansyttspp.png" width="100%" /></div>
  <figcaption>Figure 1: Overview of our proposed TTS framework. A NANSY++ model (blue) is used as the backbone model to obtain disentangled representations and convert them back to the waveform. The TTS acoustic model (red) converts text to NANSY++ features. It utilizes a style encoder and feature aggregators (aggr.) to extract style embeddings. The description control model (green) predicts style and timbre embeddings from the input text descriptions.</figcaption>
</figure>

## Comparison of different systems
### English TTS
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent. A man speaks quickly with average pitch."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/Reference/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++-w2v</th><th>ML-PromptTTS++</th><th>CL-PromptTTS++</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++-w2v/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/ML-PromptTTS++/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/ZS-NANSY-TTS-w2v/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear. A woman speaks with low pitch and normal speed."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/Reference/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++-w2v</th><th>ML-PromptTTS++</th><th>CL-PromptTTS++</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++-w2v/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/ML-PromptTTS++/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/ZS-NANSY-TTS-w2v/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent. A low-pitched man speaks slowly."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/Reference/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++-w2v</th><th>ML-PromptTTS++</th><th>CL-PromptTTS++</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++-w2v/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/ML-PromptTTS++/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/ZS-NANSY-TTS-w2v/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent. A woman speaks with normal pitch and normal speaking speed."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/Reference/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-NANSY-TTS/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++-w2v</th><th>ML-PromptTTS++</th><th>CL-PromptTTS++</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++-w2v/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/ML-PromptTTS++/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en/CL-PromptTTS++/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en/ZS-NANSY-TTS-w2v/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td></td><td></td></tr></tbody></table>

### Japanese TTS
Note that the descriptions of speaker characteristics are taken from the English references.
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent. A man speaks quickly with average pitch."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/Reference/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++</th><th>CL-PromptTTS++-w2v</th><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++-w2v/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/ZS-NANSY-TTS-w2v/260_123288_000004_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear. A woman speaks with low pitch and normal speed."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/Reference/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++</th><th>CL-PromptTTS++-w2v</th><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++-w2v/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/ZS-NANSY-TTS-w2v/1284_1180_000053_000001.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent. A low-pitched man speaks slowly."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/Reference/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++</th><th>CL-PromptTTS++-w2v</th><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++-w2v/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/ZS-NANSY-TTS-w2v/1089_134686_000021_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent. A woman speaks with normal pitch and normal speaking speed."</p>
<table><thead>
<tr><th>Reference</th><th><font color="#0000cd">CL-NANSY-TTS-w2v (ours)</font></th><th>CL-NANSY-TTS</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/Reference/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-NANSY-TTS/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>CL-PromptTTS++</th><th>CL-PromptTTS++-w2v</th><th>ZS-NANSY-TTS-w2v</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/CL-PromptTTS++-w2v/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja/ZS-NANSY-TTS-w2v/1580_141084_000031_000000.wav" type="audio/wav"></audio></td>
</tr></tbody></table>

## Style controllability samples
### Pitch control (en)
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>

### Speed control (en)
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/en_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>

### Pitch control (ja)
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent"</p>
<ol><li> He speaks with a very low pitch</li><li> He speaks with a low pitch</li><li> He speaks with a normal pitch</li><li> He speaks with a high pitch</li><li> He speaks with a very high pitch</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_p4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>

### Speed control (ja)
<p>Utterance ID: 260_123288_000004_000001</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, very middle-aged, very thick, very tensed, very powerful, bright, slightly soft, muffled, fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/260_123288_000004_000001_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1284_1180_000053_000001</p>
<p>``Descriptions of the speaker's voice are slightly masculine, feminine, very gender-neutral, adult-like, slightly thick, slightly tensed, slightly weak, bright, slightly soft, very clear"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1284_1180_000053_000001_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1089_134686_000021_000000</p>
<p>``Descriptions of the speaker's voice are very masculine, very adult-like, middle-aged, very thick, slightly tensed, slightly weak, slightly bright, slightly soft, slightly clear, slightly fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1089_134686_000021_000000_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table><p>Utterance ID: 1580_141084_000031_000000</p>
<p>``Descriptions of the speaker's voice are very feminine, adult-like, slightly middle-aged, thin, very tensed, very powerful, very bright, very hard, very clear, very fluent"</p>
<ol><li> He speaks with a very slow speaking speed</li><li> He speaks with a slow speaking speed</li><li> He speaks with a normal speaking speed</li><li> He speaks with a fast speaking speed</li><li> He speaks with a very fast speaking speed</li></ol><table><thead>
<tr><th>1</th><th>2</th><th>3</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s0.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s1.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s2.wav" type="audio/wav"></audio></td>
</tr></tbody></table><table><thead>
<tr><th>4</th><th>5</th></tr>
</thead><tbody><tr><td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s3.wav" type="audio/wav"></audio></td>
<td><audio controls=""><source src="/audio/nansyttspp/ja_style_control/CL-NANSY-TTS-w2v (ours)/1580_141084_000031_000000_s4.wav" type="audio/wav"></audio></td>
<td></td></tr></tbody></table>
