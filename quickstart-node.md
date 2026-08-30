# Node.js and TypeScript

This wrapper keeps the key on a Node.js server and provides consistent timeout and error behavior.

```ts
const baseUrl = process.env.STOCKERO_API_BASE_URL ?? 'https://pokestock.watch/api/v1';
const apiKey = process.env.STOCKERO_API_KEY;

if (!apiKey) throw new Error('STOCKERO_API_KEY is not configured');

type StockeroError = {
  error: { code: string; message: string; requestId: string };
};

export async function stockeroGet<T>(path: string): Promise<T> {
  const response = await fetch(`${baseUrl}${path}`, {
    headers: {
      Authorization: `Bearer ${apiKey}`,
      Accept: 'application/json',
      'X-Request-Id': crypto.randomUUID(),
    },
    signal: AbortSignal.timeout(8_000),
  });

  const body = await response.json();
  if (!response.ok) {
    const failure = body as StockeroError;
    console.error('Stockero request failed', {
      status: response.status,
      code: failure.error?.code,
      requestId: failure.error?.requestId,
    });
    throw new Error(failure.error?.message ?? 'Stockero request failed');
  }
  return body as T;
}
```

Use it from a server route:

```ts
const zip = '10001';
const result = await stockeroGet(
  `/stores/nearby?zip=${encodeURIComponent(zip)}&radius=25&limit=20`,
);
```

If you use Next.js, this code belongs in a server-only module, Route Handler, or Server Action. Never import it into a component containing `'use client'`.
