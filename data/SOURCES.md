# Data sources

| File | Rows | Source | Used for |
|---|---|---|---|
| `train_raw.jsonl` | 157 | Class data (ids T001–T157) | Training |
| `data_starter.xlsx` | 751 | S001–S050: class starter rows. S051–S751: written by Team Anthropic in 10 batches (`scripts/new_rows*.py`), labelled by `LABELING_GUIDE.md` | Training |
| `train_merged.jsonl` | 908 | `train_raw.jsonl` + `data_starter.xlsx`, original columns (made by `scripts/prepare_data.py`) | Checks (`scripts/check_dataset.py`) |
| `train_column_all_boost2_b10.jsonl` | 1,057 | The 908 rows as system / user / assistant columns; medium + needs_human rows repeated twice more | Training file for run 1795745604 |
| `eval_column_test50.jsonl` | 50 | `test_raw.jsonl` in system / user / assistant columns | Eval-loss graph only (run 1795748203) |
| `test_raw.jsonl` | 50 | Class test set (ids X001–X050); never trained on | Held-out test |
| `system_prompt.txt` | – | Class | System prompt for training and inference |

Class rows: 207 (157 + 50). Team-written rows: 701. No leaderboard message was copied or paraphrased.
Licence: class data used with course permission; team-written rows CC BY 4.0.
