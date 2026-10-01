# flux-catalogue

The product feed for L'Original (loriginal.org), rebuilt every night.

## What it does

A GitHub Action runs `meta_flux_catalogue.py` every day at 08:15 UTC (4:15 am in Montreal).
The script reads the public product API of loriginal.org and writes two files:

| File | Used by | Content |
|---|---|---|
| `flux/catalogue-fr.csv` | Google Merchant Center, Meta catalogue | one row per published artwork, French titles and links |
| `flux/catalogue-en.csv` | Meta catalogue only | English override (same ids, English title and link) |

If the feed did not change, nothing is committed.

## Feed URL for Google Merchant Center

```
https://raw.githubusercontent.com/Artur-art-team/flux-catalogue/main/flux/catalogue-fr.csv
```

Do not give `catalogue-en.csv` to Google. Its `override` column is a Meta format.

## Safety

- The script only reads public data. No secrets are stored here.
- If the API returns fewer than 500 artworks, the script stops and the old feed stays in place.
  A failed run shows up as a red cross in the Actions tab.

## Run it now

Actions tab, "Refresh catalogue feed", "Run workflow". Or locally:

```
pip install requests
python meta_flux_catalogue.py flux
```

## Note

GitHub pauses scheduled workflows after 60 days with no commit. The nightly feed commits keep
the repo active, but if the catalogue stops changing for two months, re-enable the workflow in
the Actions tab.
