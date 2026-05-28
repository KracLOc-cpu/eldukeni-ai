# Security

## Secrets

Do not commit private keys or backend-only tokens.

Never commit:

- Supabase service role key.
- AI provider API keys.
- Google Cloud service account JSON.
- OAuth client secrets.
- Deployment tokens.

The Supabase anon key may be used in frontend code only when Row Level Security is configured correctly.

## Access Transfer

When transferring the project:

1. Add the new owner to GitHub, Supabase, hosting, Google Apps Script and Google Cloud.
2. Confirm the new owner can run the application.
3. Rotate all private keys.
4. Remove personal billing and personal tokens.

## Reporting

Security issues should be reported privately to the current project owner. Do not publish secrets or exploit details in GitHub Issues.

