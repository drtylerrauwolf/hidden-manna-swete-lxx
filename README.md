# Hidden Manna: Swete Septuagint word data

Word-by-word data for the Greek Old Testament (the Septuagint), as used in the Hidden Manna app at [hiddenmanna.app](https://hiddenmanna.app). Every Greek word carries its dictionary number, an English gloss, a grammar tag and, where one could be matched, the Hebrew word it translates.

This repository exists to share our corrected and extended version of an openly licensed text under the same license. The app's code, design and other data are not part of it.

## Source text

- **Greek text:** Henry Barclay Swete, *The Old Testament in Greek according to the Septuagint* (Cambridge University Press, first published 1887 to 1894), as transcribed by the [First1KGreek Project](https://opengreekandlatin.github.io/First1KGreek/), licensed CC BY-SA 4.0.
- **Starting dataset:** [QuantForgeSoftware/lxx](https://github.com/QuantForgeSoftware/lxx), CC BY-SA 4.0, which adds dictionary forms and grammar tags to the First1KGreek text.
- **Word analysis:** [Morpheus](https://github.com/perseids-tools/morpheus) (MPL-2.0), as used in the starting dataset.
- **Extended Strong's numbers** (above G5624, for Greek words Strong never listed because they do not occur in the New Testament): STEPBible.org and Tyndale House, TBESG (CC BY 4.0), [stepbible.github.io/STEPBible-Data](https://stepbible.github.io/STEPBible-Data/).
- **English verse text** in the `e` field: Berean Standard Bible, public domain.

## What we changed

- Cleaned scan errors: split words rejoined, elided forms restored, stray letters and editorial scraps removed, and about 2,200 garbled words fixed or given their dictionary word, each checked against the Hebrew of its verse.
- Added a Strong's number to every word we could identify, and re-filed words that the analyzer had tagged as a different dictionary word (for example ἔλεος "mercy" tagged as ἕλος "marsh").
- Moved verses to the English verse they translate, so each Greek verse sits beside the matching English and Hebrew (for example the Greek chapter order of Jeremiah). Where Swete numbers a verse differently, the verse carries Swete's own number in `gr`.
- Paired each Greek word with the Hebrew word it translates, using a model trained on 1,790 hand-checked pairs, with the rare words matched by hand.
- Gave verbs dictionary-style or verse-specific English glosses and repaired the grammar tags (imperatives restored, tense and voice checked against the Hebrew and the New Testament).

The matching and tagging are partly automatic and are still being checked. Corrections are welcome as issues on this repository.

## Format

One file per book in `data/`, named with three-letter codes (`Gen`, `Exo`, ... `Mal`). English chapter and verse numbering. Ecclesiastes is English only for now, because this edition's Ecclesiastes has not been tagged yet.

```
{ "1": { "1": { "e": "...", "w": [ { "h": "ἀρχῇ", "g": "beginning", "p": "N-DSF", "s": 746, "hb": 7225, "hx": [[0, 1]] }, ... ] } } }
```

Each verse:

| Field | Meaning |
|---|---|
| `e` | The English verse (Berean Standard Bible) |
| `w` | The Greek words, in order |
| `gr` | Swete's own chapter:verse, when it differs from the English |
| `nm` | Set when the Greek verse does not line up word for word with the Hebrew |

Each word:

| Field | Meaning |
|---|---|
| `h` | The Greek word as it appears in the text |
| `g` | English gloss |
| `p` | Grammar tag (Robinson-style, as in STEPBible's TAGNT); `|` separates readings the form allows |
| `s` | Strong's number (Greek), including STEPBible's extended numbers |
| `hb` | Strong's number of the Hebrew word this Greek word translates |
| `hx` | Which part of the English verse translates that Hebrew word (used to bold it) |
| `hq` | `1` when the Hebrew pairing is likely rather than confirmed |
| `hr`, `hn` | For a Hebrew word that appears more than once in the verse: which occurrence this is, of how many |
| `nm`, `alt` | Notes on names, where the Greek reads a different name from the Hebrew and English |

## License

[Creative Commons Attribution-ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/). You may use, change and share this data, commercially or not, as long as you credit it and release your changes under the same license.

Suggested credit: *Swete Septuagint word data from the Hidden Manna project (The Fit Chemist LLC, CC BY-SA 4.0), based on the First1KGreek transcription of Swete (CC BY-SA 4.0).*
