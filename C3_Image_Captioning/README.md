# C3 — Image Captioning with a CNN Encoder and an LSTM Decoder

Flickr8k image-to-text generation with two frozen ImageNet backbones and a
trained LSTM decoder. **Runs on a Kaggle Notebook with a T4 GPU.**

**Notebook:** `C3_notebook.ipynb`
**Report:** `report/70173809_C3_Report.pdf`
**Seed:** 42

## How to run (Kaggle)

1. Create a Kaggle Notebook and upload `C3_notebook.ipynb`
   (File → Import Notebook).
2. Right panel → **Add Input** → Datasets → `adityajn105/flickr8k`.
3. Settings → Accelerator → **GPU T4**, Internet → **On**.
4. Run All. Expect about 20–30 minutes: two frozen backbones, two trained
   decoders, six decoding configurations.

The notebook writes `figures/`, `results/` and `c3_outputs.zip` to
`/kaggle/working`.

5. Download the executed notebook (File → Download .ipynb) and replace
   `C3_notebook.ipynb` in this folder with it.
6. Download `c3_outputs.zip` from the Output panel and extract it here so that
   `figures/` and `results/` are populated.

Locally, `data/` works instead of `/kaggle/input/flickr8k` (see
`data/README.md`), but training without a GPU is not practical.

## Method

- Split by image, seed 42: 6,000 train / 1,000 validation / 1,091 test images,
  all five captions per image kept together.
- Captions lower-cased, punctuation removed, `<start>`/`<end>` added, truncated
  to the 99th percentile (capped at 30). Vocabulary from training captions only,
  minimum frequency 5.
- Frozen ResNet-50 (2048-d) and EfficientNet-B0 (1280-d) features, cached.
- Merge decoder: image → dense (512), caption prefix → embedding (256), both
  concatenated at every step of a 512-unit LSTM, softmax over the vocabulary.
- Adam 1e-3, batch 128, dropout 0.3, up to 20 epochs, early stopping on
  validation loss (patience 3).
- Decoding: greedy, beam k=3 and beam k=5; corpus BLEU-1…4 against all five
  references.

## Artifacts produced on Kaggle

- `figures/fig1_captions_and_vocab.png` — length distribution and top words.
- `figures/fig2_loss_curves.png` — train/validation loss, both backbones.
- `figures/fig3_bleu_comparison.png` — BLEU-1…4 by backbone and decoding.
- `figures/fig4_distinct_words.png` — lexical diversity.
- `figures/fig5_examples.png` — three good and three poor test examples.
- `results/c3_dataset_stats.csv`, `c3_bleu_results.csv`, `c3_examples.csv`,
  `c3_summary.json`.
