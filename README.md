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

## Dataset organization

```text
Poster101K-v1.0/
├── images/                # Rights-verified images only
│   ├── Business/
│   ├── Culture/
│   ├── Fashion/
│   ├── Festival/
│   ├── Food/
│   └── Life/
└── annotations_withColor/
    ├── Business_annotation/xml/
    ├── Culture_annotation/xml/
    ├── Fashion_annotation/xml/
    ├── Festival_annotation/xml/
    ├── Food_annotation/xml/
    └── Life_annotation/xml/

```

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
