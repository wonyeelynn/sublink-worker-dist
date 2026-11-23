# sublink-worker-dist

Built worker bundle for deploying the sublink instance at sublink.kirinzone.xyz.

- Source: 7Sageer/sublink-worker, main commit d4e83f4 (past v2.5.0; includes #462 moving rule sets from gh-proxy.com to fastly.jsdelivr.net)
- Built with esbuild; verified locally 2026-11-24 (VLESS REALITY public-key present, XHTTP mode/path present, HY2 obfs present, zero gh-proxy.com in output)
- Known gaps: x-padding-bytes still dropped; HY2 skip-cert-verify defaults to false when the link has no insecure param

## Deploy

Cloudflare dashboard > Workers & Pages > sublink-worker > Edit code (Quick Edit) > select all, paste the full contents of worker-main-d4e83f4.js > Save and deploy. Quick Edit preserves bindings (SUBLINK_KV, custom domain). Do NOT use the "Deploy to Cloudflare Workers" button (creates a new worker).

## Verify after deploy

GET /clash?config=<base64 subscription> should return 200 with public-key present and no gh-proxy.com in the output.
