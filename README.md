# Requirements datasets

Datasets prepared within the RobustifAI project to support research on automated
requirement formalization: translating natural-language requirements into Linear
Temporal Logic (LTL) and Signal Temporal Logic (STL). They provide candidate data
for LLM fine-tuning, evaluation, and robustness studies, not verified ground truth.

## Augmented nl2spec requirements

[`nl2spec-augmented/`](nl2spec-augmented/) contains 12 CSV datasets derived from
36 natural-language/LTL pairs in the nl2spec benchmark, with 1,790 mutation rows
in total. Each file uses a different transformation, including character edits,
dictionary-based synonyms, embedding- and masked-LM-based word replacements,
contraction expansion, or number changes.

Generation used `LLMRobustnessTester` with maximum `WordEditDistance` 2,
five requested changed samples per original input, and up to 100 attempts per
original. Unchanged results were discarded; repeated changed texts were retained.
Some transformations could not mutate every input, so coverage varies by file.

The `requirement` column contains the mutated text; `formula` retains the source
LTL annotation. `Original_Requirement` identifies the original text. Other columns
record the transformation, distance measure, configured and measured input
distances, requested sample count, and sample number. `Num_Mutations` is the
requested count, not a guarantee that every original has that many rows.

## SyGuS-guided STL data

[`SyGuS/`](SyGuS/) contains `labeled_dataset.csv` and an XLSX spreadsheet version.
The CSV has 1,080 natural-language descriptions for 360 STL formulas, prepared
through the SyGuS (Syntax-Guided Synthesis)-guided `stl-nl` data-generation
approach. Its columns are `stl`, `nl`, `formula_id`, `realization_index`, and
`semantic_validation`. For future natural-language-to-STL training, `nl` is the
input and `stl` is the target. All current rows have
`semantic_validation=not_checked`.


## Acknowledgements and provenance

We gratefully acknowledge Matthias Cosler, Christopher Hahn, Daniel Mendoza,
Frederik Schmitt, and Caroline Trippel for the original
[nl2spec project and benchmark](https://github.com/realChrisHahn2/nl2spec).
The augmented LTL data derive from its
[`expert_LTL_dataset.txt`](https://github.com/realChrisHahn2/nl2spec/blob/main/datasets/expert_LTL_dataset.txt).
Please credit the original work when using these derived datasets.

See [LICENSE](LICENSE) for this repository's license and the
[upstream nl2spec MIT license](https://github.com/realChrisHahn2/nl2spec/blob/main/LICENSE)
for its original notice: `Copyright (c) 2023 Christoper Hahn`.

Funded by the European Union. Views and opinions expressed are however those of the author(s) only and do not necessarily reflect those of the European Union or the European Health and Digital Executive Agency (HADEA). Neither the European Union nor the granting authority can be held responsible for them. RobustifAI project, ID 101212818. 
