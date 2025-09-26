+++
title = 'Transcription Service'
date = '2025-09-26T21:03:00+10:00'
draft = false
+++

Follow this guide after completing the optional transcription setup steps in the main [README](/docs/getting-started).

## 1. Prepare a virtual environment

```bash
cd apps/transcription
python -m venv env
```

Activate the environment:

- **Windows**
  ```bash
  env\Scripts\activate
  ```
- **macOS/Linux**
  ```bash
  source env/bin/activate
  ```

> Using VS Code? Run `Python: Select Interpreter` and point it at `env/bin/python` (or `env\Scripts\python.exe` on Windows).

Install dependencies:

```bash
pip install -r requirements.txt
```

## 2. Configure Modal

1. Create a [Modal](https://modal.com/) account if you do not have one.
2. Authenticate the CLI:

   ```bash
   python -m modal setup
   ```

3. Run a local test (optional):

   ```bash
   modal run transcription.py
   ```

4. Deploy the transcription function:

   ```bash
   modal deploy transcription.py
   ```

## 3. Provide Cloudflare R2 secrets

The deployed function downloads audio from Cloudflare R2, transcribes it with Whisper, and deletes the object afterwards. Set these environment variables as a Modal secret:

```bash
CLOUDFLARE_ACCOUNT_ID=your-account-id
R2_ACCESS_KEY_ID=your-access-key-id
R2_SECRET_ACCESS_KEY=your-secret-access-key
R2_BUCKET_NAME=opencut-transcription
```

1. Visit the [Modal Secrets dashboard](https://modal.com/secrets/mazewinther/main).
2. Create a custom secret named `opencut-r2-secrets`.
3. Use **Import .env** and paste the variables from your `.env.local` file.

You are now ready to trigger automatic captions inside OpenCut.
