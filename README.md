# Synthetic data for 02b_load.cypher

27 CSVs with the exact headers 02b_load.cypher reads. Everything is made up: names, IDs, volumes, costs.
NPIs start with 9 so they cannot match a real prescriber. Payer and brand names are real market names used as labels only.

Load:
1. Copy the *.csv files into Neo4j's import folder.
2. Run 02a_constraints_indexes.cypher, then 02b_load.cypher.
3. Run 03_question_queries.cypher with its :params block (repId E10234, managerId E10001 exist in this data).

What's in it (Jan 3 - Sep 26, 2026, Saturday week-endings):
- 460 HCPs in 60 ZIPs / 12 CBSAs / 4 regions, 138 accounts
- 12 brands: Dry Eye (MIEBO, Xiidra, Restasis, Cyclosporine, Cequa, Vevye, Tryptyr) and Glaucoma (Vyzulta, Latanoprost, Lumigan, Rhopressa, Xalatan)
- 7 payer enterprises, 15 payer entities, 39 plans, 6 payer channels, monthly MMIT coverage
- 12 territories (Aqua, Purple, Sight x 4 geographies) + 6 district offices; 18 roster rows
- ~79K weekly Rx rows, ~24K FIA claims (9,000 patients), ~1.2K BlinkRx PAs, ~5.5K dispenses
- ~6.4K calls, ~500 rep emails, 36 speaker programs, IC results for Q1-Q3 (TRx actuals computed from the Rx data)

Stories planted so the queries return something interesting:
- MIEBO share grows from ~12% to ~18% of Dry Eye; Restasis declines.
- Humana Medicare Part D and Cigna Commercial add PA/ST to MIEBO in July 2026 (X03).
- Claims rejected for PA/step edit are retried, switched to a competitor (SUB_PRODUCT_ID), or abandoned (A09, A10, A18, X01).
- Rep in T-PU-WE (Purple West) falls behind on call plan and IC attainment in Q3 (G05, G09, X02).
- Targeted HCPs write more MIEBO / Xiidra / Vyzulta than non-targets.

Regenerate: python3 generate_synthetic_data.py <out_dir>   (fixed seed, same output every run)
