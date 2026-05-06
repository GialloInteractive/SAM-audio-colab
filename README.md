# SAM-Audio Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GialloInteractive/SAM-audio-colab/blob/main/SAM_Audio_Colab.ipynb)

Google Colab notebook for using Meta/Facebook Research SAM-Audio to separate audio sources with a text prompt.

## What It Does

- Installs SAM-Audio idempotently on Colab.
- Authenticates Hugging Face through an interactive token prompt or Colab Secret `HF_TOKEN`.
- Loads a SAM-Audio model in lightweight text-only mode to reduce memory usage.
- Supports direct upload or files from Google Drive.
- Automatically splits long audio into manageable chunks.
- Exports the isolated target, residual audio, and a zip archive of the results.

## Requirements

- Google Colab runtime with GPU. The default small model is recommended on T4;
  A100/L4-class GPUs are recommended for base or large.
- Hugging Face token with approved access to the selected SAM-Audio checkpoint.
  Each gated model repo, including `facebook/sam-audio-small`, may require
  accepting/requesting access while logged in on Hugging Face.
- Audio file supported by `torchaudio`.

## Quick Start

1. Open `SAM_Audio_Colab.ipynb` in Colab.
2. Select `Runtime > Change runtime type > GPU`.
3. Open the selected model page on Hugging Face, accept/request access, and use
   a Hugging Face read token in cell 2.
4. Run the cells from top to bottom.
5. Enter a simple English prompt, for example `man speaking`, `drums`, `guitar`.
6. Download the isolated target, the residual audio, or the final zip archive.

## Operational Notes

The notebook uses conservative settings to stay stable on Colab:

- `reranking_candidates=1`
- `predict_spans=False`
- default model `facebook/sam-audio-small`
- default chunks of 20 seconds
- text-only checkpoint filtering for optional video/ranker weights
- low-CPU-memory checkpoint loading enabled automatically on GPUs with at least
  24 GB VRAM

If model loading consumes all system RAM, keep `LOW_CPU_MEMORY_LOAD=True` in
cell 4 on A100/L4-class runtimes. On T4, use `facebook/sam-audio-small`. If you
get a GPU memory error during separation, lower `CHUNK_SECONDS` to 10.

If Hugging Face returns `401 Unauthorized` even after access was granted in the
browser, the token used by Colab is usually from a different account or an old
Colab Secret. In cell 2, keep `HF_TOKEN_SOURCE=interactive_login` and paste a
fresh read token from the same Hugging Face account that has model access.

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
