# CCODP reproducible baseline

Python/Jupyter benchmark for open-data processing and integrity verification.

## Current status

The source package was locally validated with 18 trials. Cloud execution has **not** completed and no Render measurements are reported here. Render could not fetch this private repository during the first service-creation attempt. Connect the GitHub account to Render and grant access to this repository before deploying.

## Contents

`Render_Cloud_Baseline.zip` contains the Python controller and runner, the retained benchmark implementation, nine frozen CSV inputs (38,245 rows), the source registry, input checksums and dependency requirements. Extract the archive to inspect or edit the source. It contains no credentials.

Archive SHA-256: `2fd56ead64218d9bc1a9fcaa40389953e49b34d8493a4842d94a0a71ca3129b6`

## Render configuration

Use a Python **Web Service**, the **Free** compute plan, the **Frankfurt** region and the **main** branch. No database, persistent disk, cron job or separate worker is required.

Build command:

    python -m zipfile -e Render_Cloud_Baseline.zip . && pip install --no-cache-dir -r Render_Cloud_Baseline/requirements.txt

Start command:

    cd Render_Cloud_Baseline && exec python app.py

Environment variables:

| Key | Value |
| --- | --- |
| PYTHON_VERSION | 3.12.7 |
| RUN_TOKEN | Generate a private random token with at least 32 characters in Render. Do not commit it. |
| OMP_NUM_THREADS | 1 |
| OPENBLAS_NUM_THREADS | 1 |

Health-check path: `/health`. Do not set CCODP_LOCAL_VALIDATION for the cloud experiment. The render.yaml inside the archive is for deploying the extracted source; it is not a root-level Blueprint for this archive-based repository.

## Execution and evidence

Once the service is live, open its HTTPS URL, enter the private RUN_TOKEN and select **Run benchmark**. The runner verifies input hashes and executes 30 randomized blocks, totaling 270 trials. Download the result ZIP after status becomes **completed**. Preserve the ZIP immediately: the free service has an ephemeral filesystem.

Outputs include timing CSVs, integrity checks, the executed Jupyter notebook, source code and actual environment metadata. They cover the retained subsets, not a new full-corpus cloud verification. Inspect all outputs before reporting cloud results.

The Render Python environment is not the original full Anaconda installation. The local and cloud environments have different resource limits; timing differences must not be interpreted as a controlled comparison of cloud-provider performance.

## Official references

- https://render.com/docs/free
- https://render.com/docs/web-services
- https://render.com/docs/configure-environment-variables
