# All You Need to Know About Taylor Swift Lyrics

A Python-based lyric analysis project covering 251 songs across 12 studio albums, movie soundtracks, and vault tracks. Lyrics are retrieved from the Genius API and analysed for word counts, vocabulary richness, word signatures, cosine similarity, and more.

---

## Project Structure

```
├── Retrieve_lyric_data.ipynb          # Scrapes and saves lyrics from Genius API
├── Taylor_Swift_Lyrics_Analysis.ipynb # Main analysis notebook
├── taylor_swift_genius_data.csv       # Exported lyrics dataset
├── access_token.txt                   # Genius API token (not tracked)
├── Taylor-Swift_Taylor-Swift/         # Lyrics folders per album
├── Taylor-Swift_Fearless-taylors-version/
├── ...
└── Taylor-Swift_non-album/            # Non-album tracks
```

---

## Requirements

```bash
pip install lyricsgenius requests beautifulsoup4 pandas numpy matplotlib seaborn scikit-learn nltk
```

Python 3.11+ is recommended. If you are on Python 3.10, patch `lyricsgenius/auth.py` to import `Self` from `typing_extensions` instead of `typing`.

---

## Setup

### 1. Get a Genius API Token
- Go to [https://genius.com/api-clients](https://genius.com/api-clients)
- Create a new API client (App Name is sufficient)
- Copy the **Client Access Token**
- Save it to a file called `access_token.txt` in the project root

### 2. Retrieve Lyrics
Run `Retrieve_lyric_data.ipynb` to download lyrics from Genius. Albums are downloaded one at a time to avoid timeout errors:

```python
download_album_lyrics("Taylor Swift", "Taylor-Swift")
download_album_lyrics("Taylor Swift", "Fearless-taylors-version")
# ... etc.
```

Non-album tracks (soundtracks, vault) are retrieved separately:

```python
download_non_album_lyrics("Taylor Swift", "Carolina")
download_non_album_lyrics("Taylor Swift", "Safe & Sound")
# ... etc.
```

Lyrics are saved as `.txt` files in per-album folders and exported to `taylor_swift_genius_data.csv`.

### 3. Run the Analysis
Open `Taylor_Swift_Lyrics_Analysis.ipynb` and run all cells. The notebook loads from `taylor_swift_genius_data.csv` so lyrics retrieval only needs to be done once.

---

## Analysis Overview

### I. Analysing Lyrics by Album
- Total and unique word counts per album
- Words per track and unique words per track
- Vocabulary richness ratio (unique / total words)
- Word count trends over time (2006–2025)
- TF-IDF signature words per album

### II. Analysing Words by Song
- Top songs by total word count
- Top songs by unique word ratio
- Most repetitive songs (lowest unique ratio)
- Word count distribution (histogram and boxplot)

### III. Analysing All Words over 251 Songs
- Longest words in her entire discography
- Most frequently used words (stopwords removed, length ≥ 7)
- Most common bigrams (two consecutive words)
- Bigrams where consecutive words share a boundary letter
- Word frequency by term (e.g. how many times "forever" appears per song)
- Cosine similarity between songs using TF-IDF vectors

### IV. Conclusion and Discussion

---

## Key Findings

- **Reputation** has the highest mean word count per track
- **The Life of a Showgirl** has the highest mean unique word count per track
- **The Tortured Poets Department: The Anthology** has the highest unique word ratio at 48%
- **"Miscommunications"** (17 letters) is the longest word, appearing in "Story of Us" and "Question...?"
- **"Forever"** (length ≥ 7) is the most used word across all lyrics
- **"All Too Well (10-Minute Version)"** and **"All Too Well"** are the most lyrically similar songs
- **"Dorothea"** and **"Safe & Sound"** are the second most similar pair (55% similarity)

---

## Notes

- Duplicate and non-lyric tracks (interludes, spoken word, remixes) are manually removed
- Lyrics are cleaned to remove Genius ads and section headers
- CamelCase terms (e.g. `withinBlurring`) are split at lowercase–uppercase boundaries
- Contractions (e.g. `should've`) are stripped to their root form
- Hyphenated words (e.g. `Ra-di-di-di`) are split into individual tokens
- Analysis uses Taylor's Version releases where available

---

## Acknowledgements

Inspired by [adashofdata/taylor_swift_data](https://github.com/adashofdata/taylor_swift_data). Extended to include non-album tracks, deluxe editions, and additional analyses.
