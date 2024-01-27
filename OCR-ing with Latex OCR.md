---
title: OCRizare în Obsidian
tags:
  - ocr
  - plugins
author: Nicolaie Constantinescu, kosson@gmail.com
---
# OCRizare în Obsidian

## Latex OCR

Acesta este un plugin care se folosește de infrastructura Python3 care trebuie construită la nivelul sistemului. Mai multe informații despre plugin aici: [GitHub - lucasvanmol/latex-ocr-server](https://github.com/lucasvanmol/latex-ocr-server). Tare bine prinde o placă video GForce pentru că vei avea suport de CUDA. Primul lucru care trebuie făcut este să instalezi software-ul necesar creării unui server local care rulează de pe mașina proprie. Pluginul mai permite apeluri API către un serviciu extern specializat, dar acest mod de operare este limitat la ceea ce îți oferă respectivul serviciu. Pentru scopul demonstrativ al acestui ghid de OCRizare cu Latex OCR în Obsidian, am ales rularea serverului local. 
Vom porni prin instalarea unui mediu virtual dedicat rulării aplicațiilor Python care se numește miniconda.

### Construcție infrastructură Python

Detalii de instalare a componentelor necesare în Linux/GNU distribuția Ubuntu 23.10. Primul lucru, dacă nu ai deja instalat miniconda, e timpul să o faci:

```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
```

Dacă nu ai instalat pachetul de sistem pentru pip, e timpul să-l instalezi:

```bash
sudo apt install python3-pip
```

Detaliile de instalare ale pachetelor pentru:

```bash
pip install https://github.com/lucasvanmol/latex-ocr-server/releases/download/0.1.0/latex_ocr_server-0.1.0-py3-none-any.whl
```

Se vor instala rând pe rând după cum urmează.

```text
Collecting latex-ocr-server==0.1.0
  Downloading https://github.com/lucasvanmol/latex-ocr-server/releases/download/0.1.0/latex_ocr_server-0.1.0-py3-none-any.whl (122 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 122.7/122.7 kB 885.8 kB/s eta 0:00:00
Collecting google-api-python-client~=2.107.0 (from latex-ocr-server==0.1.0)
  Downloading google_api_python_client-2.107.0-py2.py3-none-any.whl.metadata (6.6 kB)
Collecting grpcio~=1.59.2 (from latex-ocr-server==0.1.0)
  Downloading grpcio-1.59.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.0 kB)
Collecting pillow~=10.1.0 (from latex-ocr-server==0.1.0)
  Downloading Pillow-10.1.0-cp311-cp311-manylinux_2_28_x86_64.whl.metadata (9.5 kB)
Collecting torch~=2.1.0 (from latex-ocr-server==0.1.0)
  Downloading torch-2.1.2-cp311-cp311-manylinux1_x86_64.whl.metadata (25 kB)
Collecting transformers~=4.35.1 (from latex-ocr-server==0.1.0)
  Downloading transformers-4.35.2-py3-none-any.whl.metadata (123 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 123.5/123.5 kB 1.0 MB/s eta 0:00:00
Collecting httplib2<1.dev0,>=0.15.0 (from google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading httplib2-0.22.0-py3-none-any.whl (96 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 96.9/96.9 kB 1.0 MB/s eta 0:00:00
Collecting google-auth<3.0.0.dev0,>=1.19.0 (from google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading google_auth-2.27.0-py2.py3-none-any.whl.metadata (4.7 kB)
Collecting google-auth-httplib2>=0.1.0 (from google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading google_auth_httplib2-0.2.0-py2.py3-none-any.whl.metadata (2.2 kB)
Collecting google-api-core!=2.0.*,!=2.1.*,!=2.2.*,!=2.3.0,<3.0.0.dev0,>=1.31.5 (from google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading google_api_core-2.15.0-py3-none-any.whl.metadata (2.7 kB)
Collecting uritemplate<5,>=3.0.1 (from google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading uritemplate-4.1.1-py2.py3-none-any.whl (10 kB)
Collecting filelock (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading filelock-3.13.1-py3-none-any.whl.metadata (2.8 kB)
Collecting typing-extensions (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading typing_extensions-4.9.0-py3-none-any.whl.metadata (3.0 kB)
Collecting sympy (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading sympy-1.12-py3-none-any.whl (5.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.7/5.7 MB 987.1 kB/s eta 0:00:00
Collecting networkx (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading networkx-3.2.1-py3-none-any.whl.metadata (5.2 kB)
Collecting jinja2 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading Jinja2-3.1.3-py3-none-any.whl.metadata (3.3 kB)
Collecting fsspec (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading fsspec-2023.12.2-py3-none-any.whl.metadata (6.8 kB)
Collecting nvidia-cuda-nvrtc-cu12==12.1.105 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cuda_nvrtc_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (23.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 23.7/23.7 MB 696.8 kB/s eta 0:00:00
Collecting nvidia-cuda-runtime-cu12==12.1.105 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cuda_runtime_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (823 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 823.6/823.6 kB 2.4 MB/s eta 0:00:00
Collecting nvidia-cuda-cupti-cu12==12.1.105 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cuda_cupti_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (14.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.1/14.1 MB 1.4 MB/s eta 0:00:00
Collecting nvidia-cudnn-cu12==8.9.2.26 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl.metadata (1.6 kB)
Collecting nvidia-cublas-cu12==12.1.3.1 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cublas_cu12-12.1.3.1-py3-none-manylinux1_x86_64.whl (410.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 410.6/410.6 MB 4.3 MB/s eta 0:00:00
Collecting nvidia-cufft-cu12==11.0.2.54 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cufft_cu12-11.0.2.54-py3-none-manylinux1_x86_64.whl (121.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 121.6/121.6 MB 6.1 MB/s eta 0:00:00
Collecting nvidia-curand-cu12==10.3.2.106 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_curand_cu12-10.3.2.106-py3-none-manylinux1_x86_64.whl (56.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 56.5/56.5 MB 6.7 MB/s eta 0:00:00
Collecting nvidia-cusolver-cu12==11.4.5.107 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cusolver_cu12-11.4.5.107-py3-none-manylinux1_x86_64.whl (124.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.2/124.2 MB 5.9 MB/s eta 0:00:00
Collecting nvidia-cusparse-cu12==12.1.0.106 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_cusparse_cu12-12.1.0.106-py3-none-manylinux1_x86_64.whl (196.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 196.0/196.0 MB 5.0 MB/s eta 0:00:00
Collecting nvidia-nccl-cu12==2.18.1 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_nccl_cu12-2.18.1-py3-none-manylinux1_x86_64.whl (209.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 209.8/209.8 MB 4.3 MB/s eta 0:00:00
Collecting nvidia-nvtx-cu12==12.1.105 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_nvtx_cu12-12.1.105-py3-none-manylinux1_x86_64.whl (99 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 99.1/99.1 kB 3.4 MB/s eta 0:00:00
Collecting triton==2.1.0 (from torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading triton-2.1.0-0-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.whl.metadata (1.3 kB)
Collecting nvidia-nvjitlink-cu12 (from nvidia-cusolver-cu12==11.4.5.107->torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading nvidia_nvjitlink_cu12-12.3.101-py3-none-manylinux1_x86_64.whl.metadata (1.5 kB)
Collecting huggingface-hub<1.0,>=0.16.4 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading huggingface_hub-0.20.3-py3-none-any.whl.metadata (12 kB)
Collecting numpy>=1.17 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading numpy-1.26.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 5.9 MB/s eta 0:00:00
Requirement already satisfied: packaging>=20.0 in ./miniconda3/lib/python3.11/site-packages (from transformers~=4.35.1->latex-ocr-server==0.1.0) (23.1)
Collecting pyyaml>=5.1 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading PyYAML-6.0.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (2.1 kB)
Collecting regex!=2019.12.17 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading regex-2023.12.25-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (40 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 40.9/40.9 kB 10.0 MB/s eta 0:00:00
Requirement already satisfied: requests in ./miniconda3/lib/python3.11/site-packages (from transformers~=4.35.1->latex-ocr-server==0.1.0) (2.31.0)
Collecting tokenizers<0.19,>=0.14 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading tokenizers-0.15.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (6.7 kB)
Collecting safetensors>=0.3.1 (from transformers~=4.35.1->latex-ocr-server==0.1.0)
  Downloading safetensors-0.4.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.8 kB)
Requirement already satisfied: tqdm>=4.27 in ./miniconda3/lib/python3.11/site-packages (from transformers~=4.35.1->latex-ocr-server==0.1.0) (4.65.0)
Collecting googleapis-common-protos<2.0.dev0,>=1.56.2 (from google-api-core!=2.0.*,!=2.1.*,!=2.2.*,!=2.3.0,<3.0.0.dev0,>=1.31.5->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading googleapis_common_protos-1.62.0-py2.py3-none-any.whl.metadata (1.5 kB)
Collecting protobuf!=3.20.0,!=3.20.1,!=4.21.0,!=4.21.1,!=4.21.2,!=4.21.3,!=4.21.4,!=4.21.5,<5.0.0.dev0,>=3.19.5 (from google-api-core!=2.0.*,!=2.1.*,!=2.2.*,!=2.3.0,<3.0.0.dev0,>=1.31.5->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading protobuf-4.25.2-cp37-abi3-manylinux2014_x86_64.whl.metadata (541 bytes)
Collecting cachetools<6.0,>=2.0.0 (from google-auth<3.0.0.dev0,>=1.19.0->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading cachetools-5.3.2-py3-none-any.whl.metadata (5.2 kB)
Collecting pyasn1-modules>=0.2.1 (from google-auth<3.0.0.dev0,>=1.19.0->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading pyasn1_modules-0.3.0-py2.py3-none-any.whl (181 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 181.3/181.3 kB 4.6 MB/s eta 0:00:00
Collecting rsa<5,>=3.1.4 (from google-auth<3.0.0.dev0,>=1.19.0->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading rsa-4.9-py3-none-any.whl (34 kB)
Collecting pyparsing!=3.0.0,!=3.0.1,!=3.0.2,!=3.0.3,<4,>=2.4.2 (from httplib2<1.dev0,>=0.15.0->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading pyparsing-3.1.1-py3-none-any.whl.metadata (5.1 kB)
Requirement already satisfied: charset-normalizer<4,>=2 in ./miniconda3/lib/python3.11/site-packages (from requests->transformers~=4.35.1->latex-ocr-server==0.1.0) (2.0.4)
Requirement already satisfied: idna<4,>=2.5 in ./miniconda3/lib/python3.11/site-packages (from requests->transformers~=4.35.1->latex-ocr-server==0.1.0) (3.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in ./miniconda3/lib/python3.11/site-packages (from requests->transformers~=4.35.1->latex-ocr-server==0.1.0) (1.26.18)
Requirement already satisfied: certifi>=2017.4.17 in ./miniconda3/lib/python3.11/site-packages (from requests->transformers~=4.35.1->latex-ocr-server==0.1.0) (2023.11.17)
Collecting MarkupSafe>=2.0 (from jinja2->torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading MarkupSafe-2.1.4-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.0 kB)
Collecting mpmath>=0.19 (from sympy->torch~=2.1.0->latex-ocr-server==0.1.0)
  Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 7.1 MB/s eta 0:00:00
Collecting pyasn1<0.6.0,>=0.4.6 (from pyasn1-modules>=0.2.1->google-auth<3.0.0.dev0,>=1.19.0->google-api-python-client~=2.107.0->latex-ocr-server==0.1.0)
  Downloading pyasn1-0.5.1-py2.py3-none-any.whl.metadata (8.6 kB)
Downloading google_api_python_client-2.107.0-py2.py3-none-any.whl (12.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.7/12.7 MB 4.6 MB/s eta 0:00:00
Downloading grpcio-1.59.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (5.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.3/5.3 MB 5.6 MB/s eta 0:00:00
Downloading Pillow-10.1.0-cp311-cp311-manylinux_2_28_x86_64.whl (3.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.6/3.6 MB 8.2 MB/s eta 0:00:00
Downloading torch-2.1.2-cp311-cp311-manylinux1_x86_64.whl (670.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 670.2/670.2 MB 2.8 MB/s eta 0:00:00
Downloading nvidia_cudnn_cu12-8.9.2.26-py3-none-manylinux1_x86_64.whl (731.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 731.7/731.7 MB 2.6 MB/s eta 0:00:00
Downloading triton-2.1.0-0-cp311-cp311-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (89.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 89.2/89.2 MB 3.8 MB/s eta 0:00:00
Downloading transformers-4.35.2-py3-none-any.whl (7.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.9/7.9 MB 4.9 MB/s eta 0:00:00
Downloading google_api_core-2.15.0-py3-none-any.whl (121 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 122.0/122.0 kB 3.8 MB/s eta 0:00:00
Downloading google_auth-2.27.0-py2.py3-none-any.whl (186 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 186.8/186.8 kB 5.4 MB/s eta 0:00:00
Downloading google_auth_httplib2-0.2.0-py2.py3-none-any.whl (9.3 kB)
Downloading huggingface_hub-0.20.3-py3-none-any.whl (330 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 330.1/330.1 kB 7.2 MB/s eta 0:00:00
Downloading fsspec-2023.12.2-py3-none-any.whl (168 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 169.0/169.0 kB 10.0 MB/s eta 0:00:00
Downloading numpy-1.26.3-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (18.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 18.3/18.3 MB 3.8 MB/s eta 0:00:00
Downloading PyYAML-6.0.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (757 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 757.7/757.7 kB 3.5 MB/s eta 0:00:00
Downloading regex-2023.12.25-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (785 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 785.1/785.1 kB 6.2 MB/s eta 0:00:00
Downloading safetensors-0.4.2-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.3/1.3 MB 2.4 MB/s eta 0:00:00
Downloading tokenizers-0.15.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.6/3.6 MB 4.9 MB/s eta 0:00:00
Downloading typing_extensions-4.9.0-py3-none-any.whl (32 kB)
Downloading filelock-3.13.1-py3-none-any.whl (11 kB)
Downloading Jinja2-3.1.3-py3-none-any.whl (133 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 133.2/133.2 kB 3.6 MB/s eta 0:00:00
Downloading networkx-3.2.1-py3-none-any.whl (1.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 2.5 MB/s eta 0:00:00
Downloading cachetools-5.3.2-py3-none-any.whl (9.3 kB)
Downloading googleapis_common_protos-1.62.0-py2.py3-none-any.whl (228 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 228.7/228.7 kB 700.2 kB/s eta 0:00:00
Downloading MarkupSafe-2.1.4-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (28 kB)
Downloading protobuf-4.25.2-cp37-abi3-manylinux2014_x86_64.whl (294 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 294.6/294.6 kB 1.1 MB/s eta 0:00:00
Downloading pyparsing-3.1.1-py3-none-any.whl (103 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 103.1/103.1 kB 1.8 MB/s eta 0:00:00
Downloading nvidia_nvjitlink_cu12-12.3.101-py3-none-manylinux1_x86_64.whl (20.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.5/20.5 MB 4.4 MB/s eta 0:00:00
Downloading pyasn1-0.5.1-py2.py3-none-any.whl (84 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 84.9/84.9 kB 1.3 MB/s eta 0:00:00
Installing collected packages: mpmath, uritemplate, typing-extensions, sympy, safetensors, regex, pyyaml, pyparsing, pyasn1, protobuf, pillow, nvidia-nvtx-cu12, nvidia-nvjitlink-cu12, nvidia-nccl-cu12, nvidia-curand-cu12, nvidia-cufft-cu12, nvidia-cuda-runtime-cu12, nvidia-cuda-nvrtc-cu12, nvidia-cuda-cupti-cu12, nvidia-cublas-cu12, numpy, networkx, MarkupSafe, grpcio, fsspec, filelock, cachetools, triton, rsa, pyasn1-modules, nvidia-cusparse-cu12, nvidia-cudnn-cu12, jinja2, huggingface-hub, httplib2, googleapis-common-protos, tokenizers, nvidia-cusolver-cu12, google-auth, transformers, torch, google-auth-httplib2, google-api-core, google-api-python-client, latex-ocr-server
Successfully installed MarkupSafe-2.1.4 cachetools-5.3.2 filelock-3.13.1 fsspec-2023.12.2 google-api-core-2.15.0 google-api-python-client-2.107.0 google-auth-2.27.0 google-auth-httplib2-0.2.0 googleapis-common-protos-1.62.0 grpcio-1.59.3 httplib2-0.22.0 huggingface-hub-0.20.3 jinja2-3.1.3 latex-ocr-server-0.1.0 mpmath-1.3.0 networkx-3.2.1 numpy-1.26.3 nvidia-cublas-cu12-12.1.3.1 nvidia-cuda-cupti-cu12-12.1.105 nvidia-cuda-nvrtc-cu12-12.1.105 nvidia-cuda-runtime-cu12-12.1.105 nvidia-cudnn-cu12-8.9.2.26 nvidia-cufft-cu12-11.0.2.54 nvidia-curand-cu12-10.3.2.106 nvidia-cusolver-cu12-11.4.5.107 nvidia-cusparse-cu12-12.1.0.106 nvidia-nccl-cu12-2.18.1 nvidia-nvjitlink-cu12-12.3.101 nvidia-nvtx-cu12-12.1.105 pillow-10.1.0 protobuf-4.25.2 pyasn1-0.5.1 pyasn1-modules-0.3.0 pyparsing-3.1.1 pyyaml-6.0.1 regex-2023.12.25 rsa-4.9 safetensors-0.4.2 sympy-1.12 tokenizers-0.15.1 torch-2.1.2 transformers-4.35.2 triton-2.1.0 typing-extensions-4.9.0 uritemplate-4.1.1
```

Pentru verificări se pot urma instrucțiunile de aici: [Start Locally | PyTorch](https://pytorch.org/get-started/locally/#linux-verification).

În acest moment, ai la dispoziție un server dedicat pentru a realiza OCR-izarea formulelor matematice cu scopul de a le transforma în fragmente de cod LaTeX. LaTeX-ul este formatul de editare cel mai adesea folosit pentru elaborarea lucrărilor din domeniul științelor exacte. Există și alte tehnologii folosite pentru a redacta formule matematice, precum MathJAX, dar pentru acest plugin, transformarea este într-un fragment LaTeX.

## Operarea OCR-ului

În momentul în care ai infrastructura Python deja disponibilă, dacă aplicația nu a fost închisă, este timpul să o repornești. În momentul în care repornește, se inițializează serverul care gestionează întreaga operațiune de OCR-izare.

![[Screenshot from 2024-01-27 12-32-44.png]]

La prima pornire, se va descărca modelul necesar pentru a se face interpretarea imaginilor cu ajutorul algoritmilor de machine learning. Pe o mașină Linux/GNU, distribuția Ubuntu 23.10, acest model a fost descărcat în Downloads, unde a fost creat automat un subdirector `.obsidian`. În imaginea de mai sus sunt câteva detalii care vă permit să înțelegeți mai bine ceea ce s-a petrecut. Trebuie menționat că un computer cu resurse limitate de spațiu și de procesare va oferi o experiență de lucru vătămătoare nervilor operatorului. Cel puțin 8 nuclee de procesare, 16 Gb RAM și cel puțin 1T SSD-ul, ok?

Pentru exemplificare, am făcut câteva capturi de ecran a unor formule matematice dintr-o revistă de cercetare științifică - Romanian Journal of Physics, care poate fi consultată de la [Romanian Journal of Physics, vol. 47, Nos. 1-2 · Colecții BNF · Colectii BNF](https://digilib.nipne.ro/colectii/s/colectii/item/5803).

Pentru operare, va apărea o pictogramă în bara tip ribbon din stânga. 

![[Screenshot from 2024-01-27 13-14-44.png]]

Această pictogramă fiind acționată va apărea un panou simplu cu două butoane.

![[Screenshot from 2024-01-27 13-21-01.png]]

Acționând pictograma folderului, vei naviga structura directoarelor și subdirectoarelor până unde ai făcut captura de imagine a formulei pentru care dorești să faci OCRizarea. Acționarea butonului *Convert to Latex* va face această conversie care va pune rezultatul în memoria computerului. Un simplu *Paste* în editorul Obsidian sau dacă dorești în alt editor, va copia codul LaTeX și va avea drept rezultat instantaneu randarea (afișarea) rezultatului interpretării acelei secvențe de cod.

De exemplu, pentru următorul fragment de imagine capturat, avem rezultatul mai jos.

![[Screenshot from 2024-01-27 12-36-12.png]]

Se observă faptul că în ciuda calității destul de reduse a imaginii, serverul a făcut o treabă excelentă în recunoașterea conținutului. Mai jos este fragmentul LaTeX interpretat și afișat corespunzător în prezenta notă de Obsidian.

$$\begin{array}{r l}{{\mathcal{P}}=e^{-1},}&{{}{\mathrm{I}}=\operatorname*{min}_{\forall\,{\mathrm{paths}}}{\frac{2}{\hbar}}{\int_{S}{\sqrt{2m(V(R,\eta)-E)}}\,d s}}\\ {{}}&{{}}\\ {{}}&{{}=\operatorname*{min}_{\forall\,{\mathrm{paths}}}{\frac{2}{\hbar}}{\int_{0}^{1}{\sqrt{\underbrace{2m g_{i j}}_{\widetilde{B}_{i j}}(V(x_{i}(t)-E){\frac{d x_{i}}{d t}}{\frac{d x_{j}}{d t}}}}\,d t}}\end{array}$$
Un alt exemplu este imagine următoare

![[Screenshot from 2024-01-27 12-51-30.png]]

pentru care serverul a generat corect codul LaTeX.
$$\frac{d\rho(t)}{d t}\!=\!-\frac{i}{\hbar}[H,\rho(t)]\!+\!\frac{1}{2\hbar}\sum_{j}(\{V_{j}\rho(t),V_{j}^{\dagger}\}\!+\![V_{j},\rho(t)V_{j}^{\dagger}\}]).$$
Un alt exemplu ceva mai complex 

![[Screenshot from 2024-01-27 12-53-39.png]]

pentru care a fost creat corect codul necesar

$$\begin{array}{l}{{\displaystyle{\frac{d\sigma_{q q}(t)}{d t}}\!=\!-2(\lambda-\mu)\sigma_{q q}(t)+\frac{2}{m}\sigma_{p q}(t)+2D_{q q},}}\\ {{\displaystyle{\frac{d\sigma_{p p}}{d t}}\!=\!-2(\lambda+\mu)\sigma_{p p}(t)-2m\omega^{2}\sigma_{p q}(t)+2D_{p p},}}\\ {{\displaystyle{\frac{d\sigma_{p q}(t)}{d t}}\!=\!-m\omega^{2}\sigma_{q q}(t)+\frac{1}{m}\sigma_{p p}(t)-2\lambda\sigma_{p q}(t)+2D_{p q}.}}\end{array}$$

Și un ultim exemplu 

![[Screenshot from 2024-01-27 12-54-46.png]]

Pentru care a fost generat:
$$\begin{array}{l}{{T=\displaystyle\frac{1}{2i\Omega}\left(\begin{array}{c c c}{{\mu+i\Omega\,\,\,\mu-i\Omega\,}}&{{2\omega}}\\ {{\mu-i\Omega\,\,\,\mu+i\Omega\,}}&{{2\omega}}\\ {{-\omega\,\,\,\,\,\,\,-\omega\,\,\,\,\,-2\mu}}\end{array}\right),}}\\ {{K=\displaystyle\left(\begin{array}{c c c}{{-2(\lambda-i\Omega)\,\,}}&{{0\,\,\,}}&{{0}}\\ {{0\,\,\,\,\,\,-2(\lambda+i\Omega)\,\,}}&{{0}}\\ {{0\,\,\,\,\,\,\,\,0\,\,\,\,-2\lambda}}\end{array}\right)}}\end{array}$$