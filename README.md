# Deno Test

## Describing the issue

The `_shared` folder is not being recognised by Supabase when run locally within a Turborepo, causing the function to fail to book.

The `hello-world` function imports the `Test` type from `_shared/test.types.ts`. If this import is removed then the function works.

## How to replicate

```bash
# Install the Supabase CLI
# npm install supabase --save-dev
brew install supabase/tap/supabase

# Install
cd denotest
npm install

# Start Supabase
cd apps/edge
supabase start
supabase functions serve

```

Use Postman or equivalent to send a POST request to the `works-fine` function at `http://127.0.0.1:54321/functions/v1/works-fine`. You will get a valid response.

Now use Postman or equivalent to send a POST request to the `hello-world` function at `http://127.0.0.1:54321/functions/v1/hello-world`.

The error that is returned is:

```bash
{
    "code": "BOOT_ERROR",
    "message": "Worker failed to boot (please check logs)"
}
```

The only difference is one imports from the `_shared` folder.

## Cleanup

Stop Supabase

```bash
supabase stop --no-backup
```
