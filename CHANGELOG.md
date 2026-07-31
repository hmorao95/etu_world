# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `CHANGELOG.md` following the Keep a Changelog format.
- `CITATION.cff` with machine-readable citation metadata for the companion paper.
- `config/config.json` documenting the exact boolean search query, languages,
  and reporting interval used to build the index.
- `config/sources.csv` listing the media sources with coverage windows and
  importance weights.
- `data/raw/num_hits.csv` with the raw monthly article counts (matching articles
  and total articles) per source.
- `data/processed/index.csv` and `data/processed/index.xlsx` with the computed
  index (four series), extended beyond the paper's December 2024 endpoint.
- `README.md` sections: Repository Structure, Reproducing the Index (three-stage
  pipeline), a per-file Data Dictionary, How to Cite, and License.

### Changed
- Reorganized the repository into a `config/` → `data/raw/` → `data/processed/`
  pipeline layout to make index construction reproducible, with `docs/` for the
  paper and presentation materials.
- Moved `etuindex_data.xlsx` to `data/processed/` (frozen dataset published with
  the 2025 paper) and `paper.pdf` / `etu_annotated.pptx` to `docs/`.
- Relicensed the repository from the MIT License to
  Creative Commons Attribution 4.0 International (CC BY 4.0), which is the
  appropriate license for data and documentation.

## [1.0.0] - 2025-08-01

### Added
- Initial public release accompanying Morão (2025), *The economic effects of
  tensions in energy transportation*, Research in Transportation Economics,
  https://doi.org/10.1016/j.retrec.2025.101598.
- `etuindex_data.xlsx` — the ETU index data series (1969–2024).
- `etu_annotated.pptx` — annotated presentation materials.
- `paper.pdf` — the full research publication.
- `README.md`, `.gitattributes`, and `LICENSE`.
