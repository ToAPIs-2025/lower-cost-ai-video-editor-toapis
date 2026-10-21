# Project-specific integration plan

Pinned upstream: https://github.com/LudwigKienle/ai-video-production-editor/tree/6e91662888f4c99fa3b91279a62e572e2f8012d8

先给独立资产生成／导入教程和服务边界示例；完整新增 Provider 需 Settings、model router、task center、usage tracker 一起变更，按 CONTRIBUTING 先开 Feature 讨论。

Real independent image/video API results, decoded video and import-oriented recipe. The original app Settings, router, task center and timeline were not modified or accepted.

## API differences

- Bearer generation key to HTTPS `https://toapis.com` only; image `POST /v1/images/generations`, video `POST /v1/videos/generations`.
- An async task `id` is not OpenAI `data[0]`. Persist it before polling `GET /v1/images/generations/:id` or `/v1/videos/generations/:id`; wait for `completed`, then download `result.data[0].url` without forwarding credentials.
- Local first-frame upload uses `POST /v1/uploads/images`; use `image_with_roles` with `role=first_frame` only for a reviewed I2V preset. Reference editing, mask repaint and arbitrary multimodal inputs are not enabled by this example.
- Match model, quality, resolution, image count, duration, mode and audio to the exact same-key pricing rules. `billing.status=settled` and explicit costs confirm a charge; missing billing stays unknown.
- No automatic paid POST retry. Keep state/receipts private; changing a run ID can cost again.

## Remaining acceptance

1. Confirm the maintainer's desired contribution route and image/video owner.
2. Wire only the supported preset to the normal settings/registry/worker. Do not replace existing defaults or referrals.
3. Verify native create, restart/resume, readable failure, cancel semantics, download and final result placement.
4. Run upstream checks for affected modules and a real application task before calling this native integration accepted.

## Information needed from the maintainer

Target version; preferred Provider identity/configuration; native task cancellation and result persistence contract; permitted example/docs location; existing sponsorship/referral conditions.

Follow CONTRIBUTING.md: discuss a larger Provider addition in an Issue first. A future native patch must include Settings key storage, service, model router, task center, usage tracker, readiness UI and `npm run build:web`; Electron changes also need `npm run build`. These checks have not been run because no upstream application patch is published.
