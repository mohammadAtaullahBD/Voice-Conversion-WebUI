<div align="center">

<h1>Retrieval-based-Voice-Conversion-WebUI</h1>
A simple and easy-to-use voice changing framework based on VITS<br><br>

[![madewithlove](https://img.shields.io/badge/made_with-%E2%9D%A4-red?style=for-the-badge&labelColor=orange
)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)

<img src="https://counter.seku.su/cmoe?name=rvc&theme=r34" /><br>

[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/ github/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/Retrieval_based_Voice_Conversion_WebUI.ipynb)
[![Licence](https://img.shields.io/badge/LICENSE-MIT-green.svg?style=for-the-badge)](https://github.com/RVC-Project/Retrieval- based-Voice-Conversion-WebUI/blob/main/LICENSE)
[![Huggingface](https://img.shields.io/badge/🤗%20-Spaces-yellow.svg?style=for-the-badge)](https://huggingface.co/lj1995/VoiceConversionWebUI/ tree/main/)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

[**Changelog**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/docs/Changelog_CN.md) | [**FAQ** ](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98 %E8%A7%A3%E7%AD%94) | [**AutoDL·5 cents to train AI singer**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI /wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B) | [**Control Experiment record**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6% AD%8C%E6%89%8B%E6%95%99%E7%A8%8B](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5% AF%B9%E7%85%A7%E5%AE%9E%E9%AA%8C%C2%B7%E5%AE%9E%E9%AA%8C%E8%AE%B0%E5%BD%95) ) | [**Online Demo**](https://modelscope.cn/studios/FlowerCry/RVCv2demo)

[**English**](./docs/en/README.en.md) | [**中文简体**](./README.md) | [**日本语**](./docs/ jp/README.ja.md) | [**한국어**](./docs/kr/README.ko.md) ([**Korean**](./docs/kr/README.ko.han .md)) | [**Français**](./docs/fr/README.fr.md)| [**Türkçe**](./docs/tr/README.tr.md)

</div>

> The base model is trained using nearly 50 hours of open source high-quality VCTK training set. There are no copyright concerns. Please feel free to use it.

> Please look forward to the bottom model of RVCv3, which has larger parameters, larger data, better results, basically the same inference speed, and requires less training data.

<table>
    <tr>
<td align="center">Training inference interface</td>
<td align="center">Real-time voice changing interface</td>
</tr>
   <tr>
<td align="center"><img src="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/assets/129054828/092e5c12-0d49-4168-a590-0b0ef6a4f630"> </td>
     <td align="center"><img src="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/assets/129054828/730b4114-8805-44a1-ab1a-04668f3c30a6"> </td>
</tr>
<tr>
<td align="center">go-web.bat</td>
<td align="center">go-realtime-gui.bat</td>
</tr>
   <tr>
     <td align="center">You can freely choose the actions you want to perform. </td>
<td align="center">We have achieved end-to-end latency of 170ms. If you use ASIO input and output devices, you can achieve end-to-end 90ms latency, but it relies heavily on hardware driver support. </td>
</tr>
</table>

## Introduction
This warehouse has the following characteristics
+ Use top1 search to replace input source features with training set features to prevent timbre leakage
+ Fast training even on relatively poor graphics cards
+ You can get better results by using a small amount of data for training (it is recommended to collect at least 10 minutes of low-noise speech data)
+ Possibility to change timbre through model fusion (with the help of ckpt-merge in the ckpt processing tab)
+ Simple and easy to use web interface
+ UVR5 model can be called to quickly separate vocals and accompaniment
+ Use the most advanced [Vocal Pitch Extraction Algorithm InterSpeech2023-RMVPE] (#Reference Project) to eliminate the problem of mute sounds. Works best (significantly) but is faster and smaller than crepe_full
+ A card I card acceleration support

Click here to view our [Demo Video](https://www.bilibili.com/video/BV1pm4y1z7Gm/)!

## Environment configuration
The following instructions need to be executed in an environment with Python version greater than 3.8.

### Common methods for Windows/Linux/MacOS and other platforms
Choose one of the following methods.
#### 1. Install dependencies through pip
1. Install Pytorch and its core dependencies. Skip if already installed. Reference from: https://pytorch.org/get-started/locally/
```bash
pip install torch torchvision torchaudio
```
2. If it is a win system + Nvidia Ampere architecture (RTX30xx), according to the experience of #21, you need to specify the cuda version corresponding to pytorch
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
```
3. Install the corresponding dependencies according to your own graphics card
- N card
```bash
pip install -r requirements.txt
```
- A card/I card
```bash
pip install -r requirements-dml.txt
```
- A card ROCM(Linux)
```bash
pip install -r requirements-amd.txt
```
- I-Card IPEX (Linux)
```bash
pip install -r requirements-ipex.txt
```

#### 2. Install dependencies through poetry
Install the Poetry dependency management tool, skip if it is already installed. Reference from: https://python-poetry.org/docs/#installation
```bash
curl -sSL https://install.python-poetry.org | python3 -
```
Install dependencies through poetry
```bash
poetry install
```

### MacOS
Dependencies can be installed through `run.sh`
```bash
sh ./run.sh
```

## Other pre-model preparation
RVC requires some other pre-models for inference and training.

You can download these models from our [Hugging Face space](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/).

### 1. Download assets
Below is a list with the names of all pre-models and other files required for RVC. You can find scripts to download them in the `tools` folder.

- ./assets/hubert/hubert_base.pt

- ./assets/pretrained

- ./assets/uvr5_weights

If you want to use the v2 version model, you need to download it additionally.

- ./assets/pretrained_v2

### 2. Install ffmpeg
Skip if ffmpeg and ffprobe are already installed.

#### Ubuntu/Debian users
```bash
sudo apt install ffmpeg
```
#### MacOS users
```bash
brew install ffmpeg
```
#### Windows users
After downloading, place it in the root directory.
- Download [ffmpeg.exe](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffmpeg.exe)

- Download [ffprobe.exe](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffprobe.exe)

### 3. Download the files required for rmvpe vocal pitch extraction algorithm

If you want to use the latest RMVPE vocal pitch extraction algorithm, you need to download the pitch extraction model parameters and place them in the RVC root directory.

- Download [rmvpe.pt](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.pt)

#### Download the dml environment of rmvpe (optional, A card/I card users)

- Download [rmvpe.onnx](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.onnx)

### 4. AMD graphics card Rocm (optional, Linux only)

If you want to run RVC on a Linux system based on AMD's Rocm technology, please first download it here. Install the required drivers.

If you are using Arch Linux, you can use pacman to install the required drivers:
````
pacman -S rocm-hip-sdk rocm-opencl-sdk
````
For some models of graphics cards, you may need to additionally configure the following environment variables (for example: RX6700XT):
````
export ROCM_PATH=/opt/rocm
export HSA_OVERRIDE_GFX_VERSION=10.3.0
````
Also make sure your current user is in the `render` and `video` user groups:
````
sudo usermod -aG render $USERNAME
sudo usermod -aG video $USERNAME
````

## start using
### Start directly
Use the following command to start WebUI
```bash
python infer-web.py
```
### Use integration package
Download and unzip `RVC-beta.7z`
#### Windows users
Double-click `go-web.bat`
#### MacOS users
```bash
sh ./run.sh
```
### For I-card users who need to use IPEX technology (Linux only)
```bash
source /opt/intel/oneapi/setvars.sh
```

## Reference project
+ [ContentVec](https://github.com/auspicious3000/contentvec/)
+ [VITS](https://github.com/jaywalnut310/vits)
+ [HIFIGAN](https://github.com/jik876/hifi-gan)
+ [Gradio](https://github.com/gradio-app/gradio)
+ [FFmpeg](https://github.com/FFmpeg/FFmpeg)
+ [Ultimate Vocal Remover](https://github.com/Anjok07/ultimatevocalremovergui)
+ [audio-slicer](https://github.com/openvpi/audio-slicer)
+ [Vocal pitch extraction:RMVPE](https://github.com/Dream-High/RMVPE)
   + The pretrained model is trained and tested by [yxlllc](https://github.com/yxlllc/RMVPE) and [RVC-Boss](https://github.com/RVC-Boss).

## Thanks to all contributors for their efforts
<a href="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/graphs/contributors" target="_blank">
   <img src="https://contrib.rocks/image?repo=RVC-Project/Retrieval-based-Voice-Conversion-WebUI" />
</a>
