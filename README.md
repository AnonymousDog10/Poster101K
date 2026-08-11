<div align="center">

# Poster101K

**A Large-scale Multi-theme Poster Layout Dataset**

[![Posters](https://img.shields.io/badge/poster%20records-101%2C914-1F6FEB)](#dataset-composition)
[![Elements](https://img.shields.io/badge/annotated%20elements-549%2C252-1F6FEB)](#dataset-composition)
[![Themes](https://img.shields.io/badge/themes-6-2EA44F)](#dataset-composition)
[![Categories](https://img.shields.io/badge/element%20categories-9-2EA44F)](#annotation-schema)

Poster images, layout annotations, explicit underlay labels, and poster- and element-level colour palettes.

</div>

## Overview

Poster101K is a large-scale dataset for poster layout analysis and generation. The research corpus contains **101,914 poster records** from six themes and **549,252 manually annotated layout elements** from nine semantic categories. In addition to common foreground elements, Poster101K explicitly annotates underlays: background shapes or blocks used to support, group, or separate foreground content.

Poster101K also provides automatically extracted colour palettes at two levels. Each complete poster has a five-colour palette, and each annotated element crop has a three-colour palette. These annotations support research on poster geometry, layered composition, semantic element relationships, and the connection between layout and colour.

The public release is organized separately from the research corpus. Raw images will be included only for records whose redistribution basis has been verified and documented. Other eligible records may be released as annotations and metadata without the original image. 


<p align="center">
  <img src="poster101k_dataset.png" width="95%" alt="Poster101K dataset overview">
</p>


## Key features

- **Large scale:** 101,914 poster records and 549,252 annotated elements.
- **Multi-theme coverage:** food, festival, life, business, culture, and fashion.
- **Nine semantic categories:** logo, title, subtitle, underlay, text, image, caption, table, and list.
- **Explicit underlay annotations:** support the study of grouping and layered poster composition.
- **Two-level colour information:** five colours per poster and three colours per annotated element crop.
- **Manual annotation and quality control:** three annotators, written guidelines, adjudication of ambiguous cases, and a theme-stratified audit.
- **Duplicate-aware splits:** exact and near-duplicate control is completed before the 85/5/10 split is frozen.
- **Release provenance:** the planned versioned manifest records file membership, split assignment, source information, release status, and checksums.


## Dataset composition

| Theme | Poster records | Annotated elements | Elements per poster |
|---|---:|---:|---:|
| Food | 5,640 | 42,772 | 7.58 |
| Festival | 13,615 | 75,620 | 5.55 |
| Life | 23,267 | 133,716 | 5.75 |
| Business | 26,543 | 170,569 | 6.43 |
| Culture | 21,160 | 80,954 | 3.83 |
| Fashion | 11,689 | 45,621 | 3.90 |
| **Total** | **101,914** | **549,252** | **5.39** |

Element counts include underlays.

## Collection and curation

Poster candidates were retrieved from five publicly accessible design platforms. Items displayed as free by a platform were eligible for research collection, but free accessibility was not treated as evidence of permission to redistribute an image.

| Source platform | Retrieved candidates |
|---|---:|
| Wepik | 15,687 |
| Fotor | 21,463 |
| Canva | 35,312 |
| Gaoding | 24,804 |
| Pinterest | 29,358 |
| **Total** | **126,624** |

Filtering was completed before constructing the train, validation, and test subsets. Each removed poster is counted once in the first stage at which it was excluded.

| Curation stage | Removed | Remaining |
|---|---:|---:|
| Raw retrieval | -- | 126,624 |
| File-integrity filter | 9,539 | 117,085 |
| Near-duplicate removal | 7,431 | 109,654 |
| Content and quality filter | 7,740 | 101,914 |
| Final research dataset | -- | 101,914 |

The filtering process removes corrupted files, low-resolution images, incomplete canvases, invalid aspect ratios, duplicates, and low-quality content.

## Duplicate control

Exact duplicates are detected using file checksums. Resized, recompressed, cropped, and template-derived candidates are identified using perceptual hashes and normalized CLIP embeddings. A pair is flagged for review when:

- its perceptual-hash Hamming distance is at most 6; and
- its CLIP cosine similarity is at least 0.95.

Four data curators review the flagged pairs using predefined criteria for exact duplicates, template variants, and visually related but independent designs. Confirmed duplicates are removed before the official split files are frozen.

## Annotation protocol

Three annotators manually labelled Poster101K using Label Studio. Before production annotation, they reviewed a written guide covering semantic roles, box boundaries, and ambiguous cases. Each poster was assigned to one annotator, and uncertain annotations were discussed and resolved jointly.

All geometric annotations are axis-aligned rectangular boxes. Label Studio exports percentage coordinates in JSON format, which are converted into XML records containing the poster identifier, canvas dimensions, semantic category, box coordinates, and palette information. For downstream processing, every valid box can be normalized to centre coordinates, width, and height in the unit square.

## Annotation schema

| Category | Description |
|---|---|
| `logo` | Brand marks and logos |
| `title` | Primary headline text |
| `subtitle` | Secondary headline text |
| `underlay` | A shape or block whose main role is to support, group, or separate foreground content |
| `text` | General body text |
| `image` | Photographic, illustrated, or other image regions |
| `caption` | Short descriptive or explanatory text |
| `table` | Tabular content |
| `list` | Structured list content |

A full-canvas background and ordinary whitespace are not labelled as underlays. Title, subtitle, text, and caption are distinguished by their communicative roles and visual salience rather than by font size alone.

## Annotation quality control

A theme-stratified audit was performed on 300 posters covering all six themes. Corresponding elements were matched before measuring category agreement and box IoU. The audit produced:

| Measure | Result |
|---|---:|
| Category agreement | 95.6% |
| Mean bounding-box IoU | 0.88 |
| Underlay agreement | 91.3% |

Disagreements identified during the audit were reviewed and resolved jointly. The public documentation will include the annotation guide and a non-identifying quality-control summary.

## Colour palettes

Colour palettes are automatically extracted from the source poster images using Pylette:

- **Poster-level palette:** five representative colours from the complete poster.
- **Element-level palette:** three representative colours from each annotated bounding-box crop.

Palette representatives are computed as cluster means, converted to sRGB, and sorted by their assigned pixel proportions. The image-level ICAA assessment reported in the manuscript characterizes the source poster images; it does not validate palette-extraction accuracy and should not be interpreted as an aesthetic ranking of datasets.

## Spatial statistics

Poster101K supports category-pair analysis of relative element area and geometric overlap. To reduce the influence of posters containing many element pairs, statistics are first aggregated within each poster and then across posters:

- log area ratios are summarized within and across posters using the median; and
- pairwise box IoU is averaged within each poster and then across posters.

The aggregate analysis shows category-dependent relative-area patterns and higher overlap for some category pairs. Underlay-foreground pairs, in particular, exhibit more overlap than most foreground-foreground pairs. These are aggregate geometric observations; they do not encode layer order or prove that every overlap is visually desirable.

## Dataset splits

Poster101K uses a theme-stratified **85/5/10** train/validation/test split. The poster is the sampling unit, and duplicate control is completed before the split files are frozen. The same poster-level split is used for the Poster101K-NoUnderlay variant.

The versioned release will contain:

```text
splits/
└── v1.0/
    ├── train.txt
    ├── validation.txt
    ├── test.txt
    └── split_statistics.json
```

Each split file will have a published checksum, and the three subsets will be checked for disjoint membership and complete coverage of the corresponding release.

## Dataset organization

The public package is designed around a release manifest so that image availability can be distinguished from annotation and metadata availability.

```text
Poster101K-vX.Y/
├── DATA_CARD.md
├── ANNOTATION_GUIDE.md
├── DATA_LICENSE.md
├── RIGHTS.md
├── release_manifest.csv
├── release_statistics.json
├── checksums.sha256
├── images/                    # Rights-verified images only
│   ├── Business/
│   ├── Culture/
│   ├── Fashion/
│   ├── Festival/
│   ├── Food/
│   └── Life/
├── annotations/
│   ├── Business_annotation/xml/
│   ├── Culture_annotation/xml/
│   ├── Fashion_annotation/xml/
│   ├── Festival_annotation/xml/
│   ├── Food_annotation/xml/
│   └── Life_annotation/xml/
└── splits/
    └── v1.0/
```

The exact directory contents of a release are determined by `release_manifest.csv`, not by the aggregate research-corpus count.

## XML annotation example

```xml
<annotation>
  <filename>Business_1</filename>
  <category>Business</category>
  <size>
    <width>1000</width>
    <height>1779</height>
  </size>
  <palette>
    <color rgb_p="14 29 36 0.35" />
    <color rgb_p="221 225 224 0.28" />
  </palette>
  <layout>
    <element
      label="Title"
      polygon_x="77 420 420 77 77"
      polygon_y="1044 1044 1209 1209 1044"
      color_1="9 22 29 0.74"
      color_2="245 163 174 0.21"
      color_3="129 94 103 0.044" />
  </layout>
</annotation>
```

In `rgb_p`, the first three values are the sRGB components and the fourth value is the assigned pixel proportion.

## Download and verification

The stable dataset URL, release identifier, package composition, and download instructions will be added after the versioned public package has passed the release audit.

Every release will report separately:

- research-corpus records;
- records with redistributable raw images;
- records released as metadata and annotations only;
- excluded or tombstoned records; and
- annotation boxes included in the public package.

Users should verify downloaded files against `checksums.sha256` and use the release-specific manifest rather than a mutable “latest” endpoint.

## Suggested research uses

Poster101K is intended to support research on:

- graphic and poster layout analysis;
- unconditional and conditional layout generation;
- layout completion and refinement;
- poster element detection and semantic layout understanding;
- underlay-aware grouping and overlap analysis;
- theme-conditioned layout statistics;
- colour-palette analysis; and
- joint layout-and-colour generation.

The dataset is not intended to provide unrestricted commercial rights to the original poster images or to serve as a source of standalone graphic assets.

## Limitations

- Poster101K draws from five platforms and six themes, so it does not represent every poster style, language, region, or cultural setting.
- The annotations use axis-aligned rectangles and therefore do not capture irregular element boundaries.
- The nine-category schema does not encode typography, reading order, z-order, text semantics, or negative space.
- Colour palettes are automatically extracted and have not been manually validated as ground-truth colour annotations.
- Aggregate IoU measures geometric intersection but cannot distinguish intentional containment from accidental collision.
- Source-specific rights determine which original images can be redistributed in each public release.

## Rights and licensing

No single license applies automatically to every material associated with Poster101K.

- Author-created documentation, annotations, metadata, and scripts are covered only by the licenses explicitly assigned to those materials.
- Third-party poster images, when included, are not relicensed by the documentation, annotation, or code license.
- The release manifest records the source-specific status and attribution information for each public record.
- Public accessibility or a “free” label on a source platform was not treated as evidence of permission to redistribute an image.

The repository does not grant trademark, privacy, publicity, or other third-party rights not controlled by the dataset authors. Consult `DATA_LICENSE.md`, `RIGHTS.md`, and `release_manifest.csv` before using or redistributing any part of a release.

## Rights, attribution, and privacy reports

To report a rights, attribution, or privacy concern, contact the maintainers and include:

- the Poster101K record identifier;
- the relevant source or file URL;
- your relationship to the material; and
- a description of the request.

A record may be temporarily disabled while the report is reviewed. Confirmed removals will be represented as tombstones in the release manifest and recorded in the next patch release and changelog. Previously downloaded or independently mirrored copies may remain outside the maintainers' control.

## Citation

The definitive article and dataset citations will be added when public, persistent identifiers become available. Until then, the associated manuscript may be referenced as:

```bibtex
@unpublished{Wang2026Poster101K,
  author = {Fei Wang and Yang Wang and Qiuyang Yuan and Liying Wang and
            Jihong Guan and Shuigeng Zhou},
  title  = {Diffusion-based Poster Layout Generation with Aesthetic Priors:
            Dataset and Method},
  year   = {2026},
  note   = {Manuscript in preparation}
}
```

A separate dataset citation and `CITATION.cff` entry will be provided with the first stable release. No placeholder DOI should be used as a public identifier.

## Authors and contact

**Authors:** Fei Wang, Yang Wang, Qiuyang Yuan, Liying Wang, Jihong Guan, and Shuigeng Zhou.

For dataset questions or release-related reports, contact:

- Fei Wang: `wangf21@m.fudan.edu.cn`
- Shuigeng Zhou: `sgzhou@fudan.edu.cn`

## Acknowledgements

We thank the data curators and annotators of Poster101K for their contributions.

<!--
Maintainer checklist before announcing a public release:

1. Generate every count in this README from the authoritative release manifest.
2. Fill in the exact numbers of image-available, annotation-only, excluded, and
   tombstoned records.
3. Export the current dataset overview to assets/poster101k_overview.png.
4. Publish DATA_CARD.md, ANNOTATION_GUIDE.md, DATA_LICENSE.md, RIGHTS.md,
   THIRD_PARTY_NOTICES.md, TAKEDOWN.md, CHANGELOG.md, release_manifest.csv,
   release_statistics.json, and checksums.sha256.
5. Add immutable split files and verify disjointness and coverage.
6. Test the permanent download link in a clean, unauthenticated environment.
7. Create a version tag and persistent dataset record; add CITATION.cff.
8. Replace the manuscript-in-preparation citation after a public preprint or
   publisher record exists.
9. Do not display a unified license badge unless one confirmed license genuinely
   covers every artifact represented by that badge.
-->
