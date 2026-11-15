# C3 — Data source

**Dataset:** Flickr8k
**Source:** Kaggle, `adityajn105/flickr8k`
**Size:** 8,091 images, 5 captions each (40,455 captions)

Images are **not** committed to this repository. On Kaggle, attach the dataset
directly:

1. Open the notebook on Kaggle.
2. Right panel → **Add Input** → search `adityajn105/flickr8k` → Add.
3. It appears under `/kaggle/input/flickr8k/` containing:
   - `Images/` — 8,091 JPEG files
   - `captions.txt` — CSV with columns `image,caption`

For a local run, download with the Kaggle CLI:

```bash
kaggle datasets download -d adityajn105/flickr8k --unzip -p data/
```

Expected local layout:

```text
C3_Image_Captioning/
  data/
    Images/
      1000268201_693b08cb0e.jpg
      ...
    captions.txt
```

The notebook resolves the data root automatically, checking in order
`/kaggle/input/flickr8k`, `data/`, and `data/flickr8k/`.

## Split
The notebook splits **by image**, never by caption, so all five captions of an
image stay in the same split: 6,000 / 1,000 / 1,091 images (train / validation
/ test), fixed seed 42.

## Citation
M. Hodosh, P. Young and J. Hockenmaier, "Framing image description as a ranking
task: Data, models and evaluation metrics," *Journal of Artificial Intelligence
Research*, vol. 47, pp. 853-899, 2013.
