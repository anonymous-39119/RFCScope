# RFCScope

This is the artifact for _RFCScope: Detecting Logically Ambiguous Bugs in Internet Protocol Specifications_.

## This repository

### Observations from study of RFC Errata

- The `study/all_errata.md` file contains all the 273 errata that we considered in our study. For each erratum, the file contains the original text of the erratum, the RFC number, the date of the publication of the RFC, and an explanation of the erratum added by us. These errata belong to the Standards Track RFCs published from January, 2014 to January, 2025.

- The `study/categories.md` file contains the categorization of the errata in `study/all_errata.md`. We omit the errata from the _Other_ category in this file. The errata are divided into the subcategories of _Inconsistency_ and _Under-specification_.

### Evaluation

- The `evaluation/prompts` directory contains the prompts used in RFCScope for the evaluation of RFCs. This directory has the following structure.
  - `system-prompts/`: Contains the system prompts used in RFCScope.
    - `inconsistency/`: Contains the system prompts for the inconsistency analysis.
      - `analyzer.md`: The system prompt for the analyzer.
      - `evaluator.md`: The system prompt for the evaluator.
    - `under-specification/`: Contains the system prompts for the under-specification analysis.
      - `analyzer.md`: The system prompt for the analyzer.
      - `evaluator.md`: The system prompt for the evaluator.
  - `user-prompts/`: Contains the user prompts used in RFCScope. The user prompts are templates that are filled with the inputs as indicated in the file.
    - `analyzer.md`: The user prompt for the analyzer.
    - `evaluator.md`: The user prompt for the evaluator.

- The `evaluation/selected-errata/` directory contains the errata selected after manual inspection of the results from RFCScope. The directory contains a subdirectory for each RFC that has selected errata. Each errata is stored as a markdown file in the subdirectory. This file contains the errata report and its categorization. There are a total of 31 errata reports across 14 RFCs.
