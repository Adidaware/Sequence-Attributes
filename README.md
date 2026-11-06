# Sequence Attributes

A Python package that annotates human coding sequences. It reads CCDS sequences, translates them to protein, computes sequence-composition attributes, joins in gene annotations from CCDS and Ensembl, and ranks genes by proline content.

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white) ![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white) ![pytest](https://img.shields.io/badge/tested%20with-pytest-0A9EDC?logo=pytest&logoColor=white)

## ✨ What it computes

For every CCDS sequence:

* **DNA:** length, nucleotide composition, GC content, 3-mer counts
* **Protein:** translation with the standard genetic code, length, amino-acid composition, **proline content**
* **Annotation:** CCDS ID, chromosome, RefSeq gene ID, Ensembl gene ID, canonical transcript, biotype and description

The results are sorted by proline content, highest first, with ties broken by shortest protein.

## 🚀 Usage

```bash
git clone https://github.com/Adidaware/Sequence-Attributes.git
cd Sequence-Attributes
pip install -r requirements.txt

python -m sequence_attributes.main \
    --infile_ccds_fasta       CCDS_nucleotide.fna \
    --infile_ccds_attributes  CCDS.current.txt \
    --infile_ensembl_gene     ensembl_genes.tsv \
    --excel_outfile           sequence_attributes.xlsx
```

| Input | Description |
| :--- | :--- |
| `--infile_ccds_fasta` | CCDS nucleotide FASTA, with headers like `CCDS1.1\|Hs109\|chr1` |
| `--infile_ccds_attributes` | Tab-separated CCDS attribute table |
| `--infile_ensembl_gene` | Tab-separated Ensembl gene table (ID, gene, canonical transcript, biotype, description) |

**Outputs**

* `sequence_attributes.xlsx`: every sequence and its computed attributes.
* `sequence_attributes_proline_composition.tsv`: the 10 genes with the highest and the 10 with the lowest proline content (also printed to the console).

## ✅ Tests

```bash
python -m pytest
```

The tests cover the FASTA reader, the file-handling context manager and the sequence-attribute functions.

## 📁 Package Layout

```
sequence_attributes/
├── main.py                       # CLI entry point
├── sequence_formats/
│   └── fasta_format.py           # FASTA reader and validation
├── utils/
│   ├── io_utils.py               # FileHandler context manager
│   └── seq_attribute_utils.py    # composition, translation, k-mers, lookups
└── tests/unit/                   # pytest suites
```

## 📝 Notes

* Melting temperature (`tm`) is a placeholder and is always reported as `0.0`.

## 🙏 Credits

`utils/io_utils.py` is based on provided starter code.

## 👤 Author

**Aditya Daware** · [LinkedIn](https://www.linkedin.com/in/aditya-daware) · [GitHub](https://github.com/Adidaware)
