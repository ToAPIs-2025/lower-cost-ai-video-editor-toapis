# 更低成本的 AI Video Production Editor API 素材方案

[English](README.md) · [中文](README_zh-CN.md)

从剧本、分镜到素材、剪辑和导出的本地影视工作台。

这是 ToAPIs 独立维护的社区教程，不是上游官方版本。原项目：[LudwigKienle/ai-video-production-editor](https://github.com/LudwigKienle/ai-video-production-editor)；固定源码 [6e916628](https://github.com/LudwigKienle/ai-video-production-editor/tree/6e91662888f4c99fa3b91279a62e572e2f8012d8)。

## 演示

![Original API image](screenshots/cn/01-image-case.png)

[MP4 demo](assets/kling-v3-9edf6511fb.mp4) · [Video parameters and settled charge](PRICING.md)

## 费用（2026-10-21）

| 模型／条件 | 单价 | 本案例费用／来源 |
|---|---:|---|
| gemini-nano-banana-2.1 · 1K | $0.015/image | 实扣待回执；此数为同 Key 配置报价 |
| kling-v3 · std / audio=false / requested 5s | $0.059524/s in this case | $0.3 settled; 5.04s file |

[模型落地页与价格](https://x.toapis.com/1021_av_gh) · [PRICING.md](PRICING.md)

## 验证范围

真实独立图片／视频 API 输出及导入方案，视频已完整解码；原应用 Settings、路由、任务中心与时间轴尚未修改或验收。

## 调用与复用

Python 3，仅在本机私有环境配置 `TOAPIS_API_KEY`，Base 为 `https://toapis.com`（不带 `/v1`）。先查询报价，再显式添加 `--live` 提交。每次调用均核对相同 Key 的 `/v1/pricing`；通过生成响应和任务查询读取已确认 billing。

```bash
python unified_client.py --model gemini-nano-banana-2.1 --prompt-file prompts/image.txt
python unified_client.py --model gemini-nano-banana-2.1 --prompt-file prompts/image.txt --max-usd 0.10 --run-id coffee-001 --live
```

相同输入与 run-id 恢复原任务；丢失提交响应时停止并核对，不自动重发。更换 run-id 是一次新的付费任务。

[Project-specific integration](INTEGRATION.md) · [Sanitized case data](cases.json) · [Original prompts](prompts/)
