# Fugue Workshop

A single-page web app that turns a theme from a MIDI or MusicXML file into a three- or four-voice fugue.

Open `index.html` in a browser. There is nothing to install or build.

## What it does

- **Reads a theme** from `.mid`, `.midi`, `.musicxml`, `.xml` or `.mxl` files. The top melodic line becomes the subject, and the key is detected automatically (you can override it).
- **Writes the exposition**: each voice enters in turn, with a tonal answer in the dominant and a countersubject in invertible counterpoint.
- **Adds episodes** built as sequences from the subject's opening motif, often imitated in a second voice, modulating to the next key.
- **Places middle entries** in related keys (relative major or minor, subdominant).
- **Finds a stretto**: the tightest overlap of two entries that stays consonant.
- **Closes** with a final entry in the tonic and a IV–V–I cadence, with an optional Picardy third in minor keys.

You can play the fugue in the browser, view it as a piano roll or as engraved notation, and download it as MIDI and MusicXML for MuseScore, Sibelius, Logic and similar programs.

## How it works

Everything is in `index.html`:

| Part | Functions |
| --- | --- |
| File parsing | `parseMidi`, `parseMusicXML`, `normalizeTheme` |
| Key and scale-degree logic | `detectKey`, `decode`, `renderDegs`, `tonalAnswer` |
| Counterpoint engine | `genFree`: chooses a rhythm that complements the other voices, then a dynamic-programming search over pitches that penalizes strong-beat dissonance, parallel fifths and octaves, voice crossing and awkward leaps |
| Fugue planner | `buildFugue`: places entries, countersubject, episodes, stretto and cadence, then fills the remaining gaps with free counterpoint |
| Export | `toMusicXML`, `toMidi` |

## Online dependencies

Two libraries load from public CDNs: [JSZip](https://stuk.github.io/jszip/) for `.mxl` files and zip downloads, and [OpenSheetMusicDisplay](https://opensheetmusicdisplay.org/) for the Score view. Everything else works offline.

## Limitations

The counterpoint is rule-based, so expect occasional dissonances and parallels. Themes with a clear tonal outline give the best results.
