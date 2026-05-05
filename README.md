# SAM-Audio Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GialloInteractive/SAM-audio-colab/blob/main/SAM_Audio_Colab.ipynb)

Notebook Google Colab per usare SAM-Audio di Meta/Facebook Research e separare sorgenti audio tramite prompt testuale.

## Cosa fa

- Installa SAM-Audio in modo idempotente su Colab.
- Autentica Hugging Face tramite token interattivo o Colab Secret `HF_TOKEN`.
- Carica un modello SAM-Audio in modalita' leggera per ridurre la VRAM.
- Supporta upload diretto o file da Google Drive.
- Divide automaticamente audio lunghi in chunk gestibili.
- Esporta target isolato, residuo e archivio zip dei risultati.

## Requisiti

- Runtime Google Colab con GPU, preferibilmente T4 o superiore.
- Token Hugging Face con accesso approvato ai checkpoint SAM-Audio.
- File audio supportato da `torchaudio`.

## Uso rapido

1. Apri `SAM_Audio_Colab.ipynb` in Colab.
2. Seleziona `Runtime > Change runtime type > GPU`.
3. Esegui le celle dall'alto verso il basso.
4. Inserisci un prompt semplice e in inglese, per esempio `man speaking`, `drums`, `guitar`.
5. Scarica il target isolato, il residuo o lo zip finale.

## Note operative

Il notebook usa impostazioni conservative per essere stabile su Colab:

- `reranking_candidates=1`
- `predict_spans=False`
- modello predefinito `facebook/sam-audio-base`
- chunk predefiniti da 30 secondi

Se compare un errore di memoria GPU, abbassa `CHUNK_SECONDS` a 10 o 20 oppure passa a `facebook/sam-audio-small`.

## Repository upstream

Questo notebook si basa su:

- [facebookresearch/sam-audio](https://github.com/facebookresearch/sam-audio)
- [Modelli SAM-Audio su Hugging Face](https://huggingface.co/collections/facebook/sam-audio)
