# Steps to Run Our Codebase

1. Unzip `TRIAGE-Code.zip`. To install dependencies (only needed once):
   - `cd BIRD-Submission_TRIAGE_GPT-5.6-Luna`
   - `python3 -m pip install -r requirements.txt`

2. Set your OpenAI API key (from inside the `BIRD-Submission_TRIAGE_GPT-5.6-Luna` folder):
   ```bash
   export OPENAI_API_KEY="your_key_here"
   ```
   (alternatively, copy `.env.example` to `.env` and set `OPENAI_API_KEY=...` there)

3. Provide the test data where `submission_config.yaml` points:
   - Questions → `data/bird/test/test.json`
   - Databases → `data/bird/test/test_databases/<db>/<db>.sqlite`
     (databases are not shipped — see `data/bird/DATABASES.md`)

4. Run:
   ```bash
   python3 run_submission.py
   ```
   Output: BIRD-format predictions are generated and stored at `predictions/predict_test.json`.

## Notes

- The model is fixed to `gpt-5.6-luna` (OpenAI Responses API); no model configuration is needed beyond setting your own `OPENAI_API_KEY`.
- `submission_config.yaml` controls only paths, backend, and worker count (default 12).
- The first run builds a small embedding cache under `bird/cache/` (a few minutes, one time). No GPU is required.
- Resumable: re-running skips question IDs already completed (logged under `bird/runs/`), so an interrupted run resumes rather than restarting.
- Optional smoke test (no test databases needed). From the `bird/` folder, run:
  ```bash
  python3 run_full_pipeline.py --db superhero --limit 2 --workers 12
  ```
