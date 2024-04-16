# aria-amt

Efficient and robust implementation of seq-to-seq automatic piano transcription.

## Install 

Requires Python 3.11

```
git clone https://github.com/EleutherAI/aria-amt.git
cd aria-amt
pip install -e .
```

Download the preliminary model weights:

```
wget https://storage.googleapis.com/aria-checkpoints/amt/small-0.safetensors
```

## Usage

You can download mp3s from youtube using [yt-dlp](https://github.com/yt-dlp/yt-dlp):

```
yt-dlp --audio-format mp3 --extract-audio --no-playlist --audio-quality 0 <youtube-link> -o <save-path>
```

You can then transcribe using the cli: 

```
aria-amt transcribe \
    small-final \
    <path-to-checkpoint> \
    -load_path <path-to-audio> \
    -save_dir <path-to-save-dir> \
    -bs 1 \
    -compile \
    -q8
```

If you want to do batch transcription, use the `-load_dir` flag and adjust `-bs` accordingly. Compiling may take some time, but provides a significant speedup.

NOTE: Currently only bf16 is supported.

