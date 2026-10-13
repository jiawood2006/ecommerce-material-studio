# 电商素材工坊 · E-commerce Material Studio

> One-stop pipeline for e-commerce product images: category → style → scene compositing → text → QC → multi-platform delivery.

输入产品图，一条流水线出可投放的电商素材：**品类识别 → 风格匹配 → 场景感知合成 → 统一文字 → 自动质检 → 多平台尺寸适配 → 标准化交付**（含使用指南 + 清单 + zip）。

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/format-Agent%20Skill-2f6fed)](#install)
[![Part of](https://img.shields.io/badge/also%20in-hermes--skills%20collection-555)](https://github.com/jiawood2006/hermes-skills)

## Install

```bash
# 1) Agent Skills CLI (works with 50+ agent hosts)
npx skills add jiawood2006/ecommerce-material-studio

# 2) Claude Code / any host that reads ~/.claude/skills
git clone https://github.com/jiawood2006/ecommerce-material-studio.git ~/.claude/skills/ecommerce-material-studio

# 3) Hermes Agent
git clone https://github.com/jiawood2006/ecommerce-material-studio.git ~/.hermes/skills/utilities/ecommerce-material-studio
```

No build step, no account, no telemetry.

## Usage

```bash
pip install Pillow numpy scipy

# 1) detect category / style from a product photo
python3 scripts/category_detector.py --image product.png

# 2) recommend a template from category + price band + platform + brand
python3 scripts/style_matcher.py --category shampoo --platform taobao

# 3) scene-aware compositing — this is a Python library, not a CLI
python3 -c "from scripts.scene_aware_compositor import SceneAwareCompositor as C; C().composite('product.png','plan.json','out.png')"

# 4) text layer / 5) quality check / 6) platform resize / 7) delivery package
python3 scripts/text_engine.py --plan plan.json
python3 scripts/quality_check.py --plan plan.json --image out.png
python3 scripts/platform_adapter.py --input out.png --platform taobao
python3 scripts/delivery_packager.py --dir ./out

# 8) batch mode with resume
python3 scripts/batch_processor.py --input-dir ./products --plan plan.json
```
10 modules: `category_detector` `style_matcher` `scene_aware_compositor` `text_engine` `quality_check` `platform_adapter` `layout_engine` `brand_loader` `preference_memory` `delivery_packager`.
Data files live in [`references/`](references/): category templates, product profiles, brand config template.

## Requirements

Python 3.9+ with `Pillow numpy scipy`.

## Notes

`SceneAwareCompositor` is a **library**, not a command-line tool — call it from Python (see above). Brand assets are configuration, not shipped logos: bring your own.

## License

MIT — see [LICENSE](LICENSE). Issues and PRs welcome.
Part of the [hermes-skills](https://github.com/jiawood2006/hermes-skills) collection.
