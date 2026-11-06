# CCODP reproducible baseline

Python/Jupyter source package and frozen inputs for open-data processing and canonical textual integrity verification.

## Scope and evidence status

This repository contains the benchmark implementation and nine frozen CSV input subsets. It is not, by itself, the complete archive of the measurements reported in the associated manuscript.

A Render web service named `ccodp-python-baseline` is configured against this repository in **Oregon, USA**, using the Python runtime and Free compute plan. This configuration was checked on 6 November 2026. The older README described a preliminary deployment attempt and incorrectly presented that initial status as current.

The manuscript reports an initial local session, a Render session on 22 October 2026, and an additional Render session on 29 October 2026. The original session-specific result archives, local full-corpus data, raw metadata responses, and inferential-analysis outputs are **not included in this repository** at this revision. Their numerical findings must be checked against the preserved supplementary archives. No new timing results were generated for this documentation update.

The `validation_status.json` inside the source ZIP records **18 local software-validation trials before deployment**. It is historical package validation, not evidence of the later cloud experiments.

## Contents and provenance

`Render_Cloud_Baseline.zip` contains:

- The authenticated Python web controller and execution runner.
- The retained CSV/SQLite benchmark implementation.
- Nine frozen CSV inputs containing **38,245 data rows** in total.
- Input SHA-256 checksums, a source registry, dataset profiles, and dependency requirements.
- A configuration template and the historical local-validation status.

Archive SHA-256:

`2fd56ead64218d9bc1a9fcaa40389953e49b34d8493a4842d94a0a71ca3129b6`

The source archive was introduced in commit `00f41c350a4378484ecd46af416c9f913c60c8d4` and is also present unchanged at manuscript-associated commit `6f962e5073e7a92589bf019bd2716c188bfc9f6b`. Documentation updates do not change that historical source archive.

The inputs originate from NYC Open Data, Chicago Data Portal, and Eurostat. Original dataset identifiers, source URLs, and reuse notices are recorded in `metadata/source_registry.json`. Dataset reuse remains subject to the respective source terms; no blanket new data licence is asserted here.

## Render configuration

The existing service uses the **Oregon** region, **main** branch, Python runtime, and Free compute plan.

Build command:

    python -m zipfile -e Render_Cloud_Baseline.zip . && pip install --no-cache-dir -r Render_Cloud_Baseline/requirements.txt

Start command:

    cd Render_Cloud_Baseline && exec python app.py

Environment variables:

| Key | Value |
| --- | --- |
| PYTHON_VERSION | 3.12.7 |
| RUN_TOKEN | Set a private random token of at least 32 characters in Render. Never commit it. |
| OMP_NUM_THREADS | 1 |
| OPENBLAS_NUM_THREADS | 1 |

The application implements `/health`. The existing service configuration did not specify a health-check path at the time of inspection. Do not set `CCODP_LOCAL_VALIDATION` for a cloud experiment. The `render.yaml` inside the ZIP applies to the extracted source and is not a root-level Blueprint for this archive-based repository.

## Running a new experiment

Open the service URL, enter the private run token, and select **Run benchmark**. The runner verifies the frozen input hashes and executes 30 randomized blocks across nine datasets: **270 dataset-level trials** and **810 operation-level timings**.

Download the results ZIP once the run status is completed. Preserve it before a restart, redeployment, or service sleep because the service filesystem is ephemeral. A new execution produces new observations; it does not recreate the exact historical timing values. Keep every session in a separately named archive and retain its environment record.

Generated outputs include timing CSVs, integrity checks, an executed notebook, source files, and environment metadata. They cover the retained subsets, not a full-corpus cloud verification.

## Interpretation

The timed operations are CSV reading, in-memory SQLite import, and SQL readback. Input identity and textual integrity are separate from semantic validity and full application portability. Local and Render measurements should be interpreted with their actual software versions, resource limits, cache conditions, and session design. The benchmark does not measure live portal usability, provider-wide performance, scalability, or costs.

## Citation

Hyseni, B. (2026). *CCODP reproducible baseline* [Computer software]. GitHub. https://github.com/bhyseni1/ccodp-reproducible-baseline

When referencing the historical implementation, identify commit `6f962e5073e7a92589bf019bd2716c188bfc9f6b` and the ZIP checksum above. No archival DOI is claimed.

## Official documentation

- https://render.com/docs/free
- https://render.com/docs/web-services
- https://render.com/docs/configure-environment-variables
- https://render.com/docs/deploys
