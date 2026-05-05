# SAM-Audio Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GialloInteractive/SAM-audio-colab/blob/main/SAM_Audio_Colab.ipynb)

Google Colab notebook for using Meta/Facebook Research SAM-Audio to separate audio sources with a text prompt.

## What It Does

- Installs SAM-Audio idempotently on Colab.
- Authenticates Hugging Face through an interactive token prompt or Colab Secret `HF_TOKEN`.
- Loads a SAM-Audio model in lightweight mode to reduce VRAM usage.
- Supports direct upload or files from Google Drive.
- Automatically splits long audio into manageable chunks.
- Exports the isolated target, residual audio, and a zip archive of the results.

## Requirements

- Google Colab runtime with GPU, preferably T4 or better.
- Hugging Face token with approved access to the SAM-Audio checkpoints.
- Audio file supported by `torchaudio`.

## Quick Start

1. Open `SAM_Audio_Colab.ipynb` in Colab.
2. Select `Runtime > Change runtime type > GPU`.
3. Run the cells from top to bottom.
4. Enter a simple English prompt, for example `man speaking`, `drums`, `guitar`.
5. Download the isolated target, the residual audio, or the final zip archive.

## Operational Notes

The notebook uses conservative settings to stay stable on Colab:

- `reranking_candidates=1`
- `predict_spans=False`
- default model `facebook/sam-audio-base`
- default chunks of 30 seconds

If you get a GPU memory error, lower `CHUNK_SECONDS` to 10 or 20, or switch to `facebook/sam-audio-small`.

## Upstream Repository

This notebook is based on:

- [facebookresearch/sam-audio](https://github.com/facebookresearch/sam-audio)
- [SAM-Audio models on Hugging Face](https://huggingface.co/collections/facebook/sam-audio)

## License

The original notebook and documentation in this repository are licensed under
the [MIT License](LICENSE).

SAM-Audio itself, including model code and checkpoints cloned or downloaded at
runtime, is developed by Meta/Facebook Research and licensed separately under
the SAM License. Users must request checkpoint access on Hugging Face and comply
with the applicable SAM-Audio license terms. See
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for details.
