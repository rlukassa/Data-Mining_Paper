# Association Mining of Cross-Conference Publication Patterns in DBLP: A Temporal Analysis (2015–2025)

This project performs frequent pattern mining and association rule analysis on DBLP conference publication records to discover cross-conference co-publication patterns among researchers. The analysis covers four temporal periods from 2015 to 2025 and uses two transactional representations — author-based and author-year-based — to compare frequent itemsets and association rules, and to track how those patterns shift across time.

## Data

The dataset is sourced from the [DBLP Computer Science Bibliography](https://dblp.org/), a curated bibliographic database of computer science publications. The raw data is the DBLP XML dump (`dblp.xml.gz`), which is downloaded automatically by the analysis notebook on first run.

- **Period:** 2015–2025
- **Records used:** `inproceedings` entries (conference and workshop papers) only
- **Preprocessing:** missing-value removal, year filtering, front-matter stripping, venue normalization, author deduplication, duplicate removal
- **Final dataset statistics** are computed in Task 1.5 of the notebook


> Most scripts and analysis outputs can be left as-is; they do not take up substantial space. However, the raw DBLP XML file (~few GB) is downloaded automatically and should be treated as described above.

## Getting Started

The primary analysis entry point is the Jupyter notebook:

```
src/conference-popularity-analysis.ipynb
```

To rerun the full analysis from scratch:

1. Open the notebook in Jupyter:
   ```bash
   jupyter notebook src/conference-popularity-analysis.ipynb
   ```
2. Run all cells sequentially. Task 1 will download and preprocess the DBLP data automatically; Tasks 2–4 will execute the analyses and produce visualizations saved to `docs/`.

### Example

To load the cleaned dataset and inspect basic statistics:

```python
import pandas as pd
papers = pd.read_parquet(f"{DATA_DIR}/clean/papers.parquet")
pa = pd.read_parquet(f"{DATA_DIR}/clean/paper_author.parquet")
print(f"Papers: {len(papers)}, Authors: {pa['a'].nunique()}, Venues: {papers['venue'].nunique()}")
```

## Requirements

A step-by-step guide to setting up the development/analysis environment:

1. **Python 3.10+** recommended
2. Install required packages:
   ```bash
   pip install lxml pyarrow mlxtend matplotlib pandas numpy scipy
   ```
3. Clone the repository and navigate to the project directory:
   ```bash
   git clone https://github.com/rlukassa/Data-Mining_Paper
   cd Data-Mining_Paper
   ```
4. Open and run the notebook:
   ```bash
   jupyter notebook src/conference-popularity-analysis.ipynb
   ```

## Publications

- **[Paper]** *Association Mining of Cross-Conference Publication Patterns in DBLP: A Temporal Analysis (2015–2025)* — Data Mining course project.

## Contributing

This is an academic project. If you would like to contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -am 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

Please follow consistent coding style (PEP 8 for Python, clear markdown for notebook cells) and include comments explaining analysis steps.

## Notes

- The DBLP XML file is large (~few GB); the notebook uses streaming parsing to handle it efficiently.
- The minimum venue-paper threshold for transactional items is set to **200** (see Task 1.5 and Task 3 for rationale).
- Two transactional representations are constructed: **Author-Based** (1 transaction = 1 author, items = venues) and **Author-Year-Based** (1 transaction = 1 author-year pair).
- The Apriori algorithm is implemented from scratch (bitset-based support counting) in addition to using `mlxtend`.
- All figures are saved to `docs/` and embedded in the notebook.

## Authors

- **Lukas Raja Agripa** - Initial work - lukasagripa27@gmail.com
- **Zahran Nizar Fadhlan** - Initial work - zahrannizarfadhlan@gmail.com

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.

## Acknowledgments

- DBLP bibliography data is provided by the [Schloss Dagstuhl – Leibniz-Zentrum für Informatik](https://dblp.org/) and is licensed under CC BY 4.0.
- Analysis methods inspired by standard data mining coursework on frequent pattern mining and association rule learning.
