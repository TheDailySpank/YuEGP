<p align="center">
    <img src="./assets/logo/白底.png" width="400" />
</p>

<p align="center">
    <a href="https://map-yue.github.io/">Demo 🎶</a> &nbsp;|&nbsp; 📑 <a href="">Paper (coming soon)</a>
    <br>
    <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-en-cot">YuE-s1-7B-anneal-en-cot 🤗</a> &nbsp;|&nbsp; <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-en-icl">YuE-s1-7B-anneal-en-icl 🤗</a> &nbsp;|&nbsp; <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-jp-kr-cot">YuE-s1-7B-anneal-jp-kr-cot 🤗</a>
    <br>
    <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-jp-kr-icl">YuE-s1-7B-anneal-jp-kr-icl 🤗</a> &nbsp;|&nbsp; <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-zh-cot">YuE-s1-7B-anneal-zh-cot 🤗</a> &nbsp;|&nbsp; <a href="https://huggingface.co/m-a-p/YuE-s1-7B-anneal-zh-icl">YuE-s1-7B-anneal-zh-icl 🤗</a>
    <br>
    <a href="https://huggingface.co/m-a-p/YuE-s2-1B-general">YuE-s2-1B-general 🤗</a> &nbsp;|&nbsp; <a href="https://huggingface.co/m-a-p/YuE-upsampler">YuE-upsampler 🤗</a>
</p>

---
Our model's name is **YuE (乐)**. In Chinese, the word means "music" and "happiness." Some of you may find words that start with Yu hard to pronounce. If so, you can just call it "yeah." We wrote a song with our model's name.

<audio controls src="https://cdn-uploads.huggingface.co/production/uploads/6555e8d8a0c34cd61a6b9ce3/rG-ELxMyzDU7zH-inB9DV.mpga"></audio>

YuE is a groundbreaking series of open-source foundation models designed for music generation, specifically for transforming lyrics into full songs (lyrics2song). It can generate a complete song, lasting several minutes, that includes both a catchy vocal track and complementary accompaniment, ensuring a polished and cohesive result. YuE is capable of modeling diverse genres/vocal styles. Below are examples of songs in the pop and metal genres. For more styles, please visit the demo page.

Pop:Quiet Evening
<audio controls src="https://cdn-uploads.huggingface.co/production/uploads/640701cb4dc5f2846c91d4eb/gnBULaFjcUyXYzzIwXLZq.mpga"></audio>
Metal: Step Back
<audio controls src="https://cdn-uploads.huggingface.co/production/uploads/6555e8d8a0c34cd61a6b9ce3/kmCwl4GRS70UYDEELL-Tn.mpga"></audio>

## YuE GP for the GPU Poor by DeepBeepMeep

Please first follow the instructions to install the app below.

To run the Gradio app with a profile 3 (default profile, the fastest but requires 16 GB of VRAM):
```bash
cd inference
python gradio_app --profile 1
```

To run the Gradio app with a profile 3 (default profile, a bit slower and the model is quantized to 8 bits but requires 12 GB of VRAM):
```bash
cd inference
python gradio_app --profile 3
```

To run the Gradio app with less than 10 GB of VRAM  profile 4 (very slow as this will incur sequencial offloading):
```bash
cd inference
python gradio_app --profile 4
```

If you have a Linux based system / Windows WSL or  were able to install Triton on Windows, you can also turn on Pytorch compilation with '--compile' for a faster generation.  
```bash
cd inference
python gradio_app --profile 4 --compile
```
To install Triton on Windows: https://github.com/woct0rdho/triton-windows/releases/download/v3.1.0-windows.post8/triton-3.1.0-cp310-cp310-win_amd64.whl

Likewise if you were not able to install flash attention on Windows, you can force the application to use sdpa attention instead by using the '--sdpa' switch. Be aware that this may requires more VRAM
```bash
cd inference
python gradio_app --profile 4 --sdpa
```


You may check the mmgp git homepage  (https://github.com/deepbeepmeep/mmgp)  if you want to design your own profiles.

If you enjoy this application, you will certainly appreciate these ones too:
- Hunyuan3D-2GP: https://github.com/deepbeepmeep/Hunyuan3D-2GP\
A great image to 3D or text to 3D tool by the Tencent team. Thanks to mmgp it can run with less than 6 GB of VRAM

- HuanyuanVideoGP: https://github.com/deepbeepmeep/HunyuanVideoGP\
One of the best open source Text to Video generator

- FluxFillGP: https://github.com/deepbeepmeep/FluxFillGP\
One of the best inpainting / outpainting tools based on Flux that can run with less than 12 GB of VRAM.

- Cosmos1GP: https://github.com/deepbeepmeep/Cosmos1GP\
This application include two models: a text to world generator and a image / video to world (probably the best open source image to video generator).

- OminiControlGP: https://github.com/deepbeepmeep/OminiControl1GP\
A flux derived image generator that will allow you to transfer an object of your choosing in a prompted scene. It is optimized to run with ony 6 GB of VRAM.

## News and Updates
* **2025.01.30 🔥**: DeepBeepMeep: Speed improvements for low VRAM profiles + patch for transformers library.
* **2025.01.29 🔥**: DeepBeepMeep: GPU Poor version.
* **2025.01.26 🔥**: We have released the **YuE** series.

<br>

## Requirements



~Python >=3.8 is recommended.~

```
conda create -n yuegp python=3.11
conda activate yuegp
```

Install dependencies with the following command:

```
pip install -r requirements.txt
```

### **Important: Install FlashAttention 2**
For saving GPU memory, **FlashAttention 2 is mandatory**. Without it, large sequence lengths will lead to out-of-memory (OOM) errors, especially on GPUs with limited memory. Install it using the following command:
```
pip install flash-attn --no-build-isolation
```
Before installing FlashAttention, ensure that your CUDA environment is correctly set up. 
For example, if you are using CUDA 11.8:
- If using a module system:
``` module load cuda11.8/toolkit/11.8.0 ```
- Or manually configure CUDA in your shell:
```
    export PATH=/usr/local/cuda-11.8/bin:$PATH
    export LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH
```

---

## GPU Memory Usage and Sessions

YuE requires significant GPU memory for generating long sequences. Below are the recommended configurations:

- **For GPUs with 24GB memory or less**: Run **up to 2 sessions** concurrently to avoid out-of-memory (OOM) errors.
- **For full song generation** (many sessions, e.g., 4 or more): Use **GPUs with at least 80GB memory**. This can be achieved by combining multiple GPUs and enabling tensor parallelism.

To customize the number of sessions, the interface allows you to specify the desired session count. By default, the model runs **2 sessions** for optimal memory usage.

---

## Quickstart

```
# Make sure you have git-lfs installed (https://git-lfs.com)
git lfs install
git clone https://github.com/deepbeepmeep/YuEGP/

cd YuEGP/inference/
git clone https://huggingface.co/m-a-p/xcodec_mini_infer
```

If you have no choice but to use a low VRAM profile (profile 3 or 5), I am providing a patch for the transformers libray that should double the speed of the transformers libary (note this patch offers little little improvements on other profiles), this patch overwrites two files from the transformers libary. You can either copy and paste my 'transformers' folder in your venv or run the script below if the venv directory is just below the app directory:

For Linux:
```
source patchtransformers.sh
```

For Windows:
```
patchtransformers.bat
```

Here’s a quick guide to help you generate music with **YuE** using 🤗 Transformers. Before running the code, make sure your environment is properly set up, and that all dependencies are installed.

### Running the Script

In the following example, customize the `genres` and `lyrics` in the script, then execute it to generate a song with **YuE**.

Notice: Set `--run_n_segments` to the number of lyric sections if you want to generate a full song. Additionally, you can increase `--stage2_batch_size` based on your available GPU memory.

```bash
cd YuE/inference/
python infer.py \
    --stage1_model m-a-p/YuE-s1-7B-anneal-en-cot \
    --stage2_model m-a-p/YuE-s2-1B-general \
    --genre_txt prompt_examples/genre.txt \
    --lyrics_txt prompt_examples/lyrics.txt \
    --run_n_segments 2 \
    --stage2_batch_size 4 \
    --output_dir ./output \
    --cuda_idx 0 \
    --max_new_tokens 3000 
```

If you want to use audio prompt, enable `--use_audio_prompt`, and provide audio prompt:
```bash
cd YuE/inference/
python infer.py \
    --stage1_model m-a-p/YuE-s1-7B-anneal-en-icl \
    --stage2_model m-a-p/YuE-s2-1B-general \
    --genre_txt prompt_examples/genre.txt \
    --lyrics_txt prompt_examples/lyrics.txt \
    --run_n_segments 2 \
    --stage2_batch_size 4 \
    --output_dir ./output \
    --cuda_idx 0 \
    --max_new_tokens 3000 \
    --audio_prompt_path {YOUR_AUDIO_FILE} \
    --prompt_start_time 0 \
    --prompt_end_time 30 
```


---

### **Execution Time**
On an **H800 GPU**, generating 30s audio takes **150 seconds**.
On an **RTX 4090 GPU**, generating 30s audio takes approximately **360 seconds**.  

**Tips:**
1. `genres` should include details like instruments, genre, mood, vocal timbre, and vocal gender.
2. The length of `lyrics` segments and the `--max_new_tokens` value should be matched. For example, if `--max_new_tokens` is set to 3000, the maximum duration for a segment is around 30 seconds. Ensure your lyrics fit this time frame.
3. If using audio prompt，the duration around 30s will be fine.
---

### Notice
1. A suitable [Genre] tag consists of five components: genre, instrument, mood, gender, and timbre. All five should be included if possible, separated by spaces. The values of timbre should include "vocal" (e.g., "bright vocal").

2. Although our tags have an open vocabulary, we have provided the 200 most commonly used [tags](./wav_top_200_tags.json). It is recommended to select tags from this list for more stable results.

3. The order of the tags is flexible. For example, a stable genre control string might look like: "[Genre] inspiring female uplifting pop airy vocal electronic bright vocal vocal."

4. Additionally, we have introduced the "Mandarin" and "Cantonese" tags to distinguish between Mandarin and Cantonese, as their lyrics often share similarities.

## License Agreement

Creative Commons Attribution Non Commercial 4.0

---

## Citation

If you find our paper and code useful in your research, please consider giving a star :star: and citation :pencil: :)

```BibTeX
@misc{yuan2025yue,
  title={YuE: Open Music Foundation Models for Full-Song Generation},
  author={Ruibin Yuan and Hanfeng Lin and Shawn Guo and Ge Zhang and Jiahao Pan and Yongyi Zang and Haohe Liu and Xingjian Du and Xeron Du and Zhen Ye and Tianyu Zheng and Yinghao Ma and Minghao Liu and Lijun Yu and Zeyue Tian and Ziya Zhou and Liumeng Xue and Xingwei Qu and Yizhi Li and Tianhao Shen and Ziyang Ma and Shangda Wu and Jun Zhan and Chunhui Wang and Yatian Wang and Xiaohuan Zhou and Xiaowei Chi and Xinyue Zhang and Zhenzhu Yang and Yiming Liang and Xiangzhou Wang and Shansong Liu and Lingrui Mei and Peng Li and Yong Chen and Chenghua Lin and Xie Chen and Gus Xia and Zhaoxiang Zhang and Chao Zhang and Wenhu Chen and Xinyu Zhou and Xipeng Qiu and Roger Dannenberg and Jiaheng Liu and Jian Yang and Stephen Huang and Wei Xue and Xu Tan and Yike Guo}, 
  howpublished={\url{https://github.com/multimodal-art-projection/YuE}},
  year={2025},
  note={GitHub repository}
}
```
<br>
