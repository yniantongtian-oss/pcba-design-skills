<div align="center">

![PCBA Design Skills workflow built from real nescart schematic, PCB, and placement artifacts](assets/banner.png)

# PCBA Design Skills

**A modular, evidence-gated electronics design toolkit for engineering assistants.**

[![Validate](https://github.com/Keitark/pcba-design-skills/actions/workflows/validate.yml/badge.svg)](https://github.com/Keitark/pcba-design-skills/actions/workflows/validate.yml)
[![Release](https://img.shields.io/github/v/release/Keitark/pcba-design-skills?label=release)](https://github.com/Keitark/pcba-design-skills/releases)
[![MIT code](https://img.shields.io/badge/code-MIT-55d6be.svg)](LICENSE)
[![CC BY-SA case study](https://img.shields.io/badge/case%20study-CC%20BY--SA%204.0-f4b942.svg)](ASSET-LICENSES.md)
[![8 modular skills](https://img.shields.io/badge/skills-8-39c6f4.svg)](#choose-one-skill-or-the-whole-team)
[![English](https://img.shields.io/badge/docs-English-8b5cf6.svg)](README.md)

[Choose a skill](docs/choose-a-skill.md) · [Install](docs/installation.md) · [Record a demo](docs/recorded-workflow.md) · [nescart case study](docs/case-study-nescart.md)

</div>

PCBA Design Skills turns an idea, circuit description, native schematic,
netlist-like drawing, PCB, BOM, or fabrication package into a sequence of
reviewable engineering artifacts. Use one specialist for a focused job or the
manager for the complete design-to-order workflow.

The suite does not confuse a clean drawing with a correct circuit, zero opens
with a releasable PCB, or a successful upload with correct assembly placement.
Every stage has explicit evidence and invalidation rules.

## Choose one skill or the whole team

| Skill | Use it for | Main artifact |
|---|---|---|
| [`manage-pcba-program`](.agents/skills/manage-pcba-program/SKILL.md) | End-to-end coordination and gate tracking | `program-state.json` |
| [`plan-electronic-product`](.agents/skills/plan-electronic-product/SKILL.md) | Turning behavior and constraints into engineering inputs | `product-brief.yaml`, `architecture.md` |
| [`qualify-pcba-sourcing`](.agents/skills/qualify-pcba-sourcing/SKILL.md) | Exact MPN, package, stock, cost, CAD, and substitution review | `sourcing-lock.csv` |
| [`design-and-review-circuit`](.agents/skills/design-and-review-circuit/SKILL.md) | Circuit correctness, power, timing, states, protection, and constraints | `circuit-review.md` |
| [`schematic-humanizer`](.agents/skills/schematic-humanizer/SKILL.md) | Visible wiring, buses, functional sheets, overlap removal, and visual QA | readable source, PDF/PNG, connectivity comparison |
| [`pcb-layout-review`](.agents/skills/pcb-layout-review/SKILL.md) | Placement, derivative variants, routing, references, planes, DRC, mechanics, and DFM | `layout-review.json`, experiment ledger |
| [`release-pcba-fabrication`](.agents/skills/release-pcba-fabrication/SKILL.md) | Revision-consistent Gerber, drill, BOM, CPL, and release evidence | `release-manifest.json` |
| [`operate-jlcpcb-order`](.agents/skills/operate-jlcpcb-order/SKILL.md) | JLCPCB quote, matching, CPL preview, optional physical stencil, cost, cart, and approval gates | placement/quote/order records |

[The selection guide](docs/choose-a-skill.md) includes input-based examples and
shows which skills can be used without the manager.

## Workflow

```mermaid
flowchart LR
    A["Idea / description"] --> B["Product brief"]
    N["Schematic / netlist"] --> H["Humanized schematic"]
    B --> S["Sourcing lock"]
    H --> C["Circuit review"]
    S --> C
    C --> L["PCB layout"]
    L --> R["Fabrication release"]
    R --> J["JLCPCB review"]
    J --> G{"User approvals"}
```

All interoperable artifacts default to `.pcba-workflow/` and use `PASS`,
`BLOCKED`, or `USER_REVIEW`. A changed netlist, MPN/package, footprint,
placement, routing, BOM, CPL, or browser placement invalidates its downstream
gates; see [artifact contracts](docs/artifact-contracts.md).

## Installation and usage

The eight roles are available in `.agents/skills/` as self-contained `SKILL.md` specifications. See the [installation guide](docs/installation.md) for environment-specific setup, updates, removal, and verification.

For a complete workflow, begin with `manage-pcba-program`. Supply the existing circuit description, schematic, netlist, PCB and bill of materials. The manager creates project state, delegates the required reviews, and stops at unresolved engineering or user-approval gates.

For a narrow task, select only the relevant specialty, such as `schematic-humanizer` or `pcb-layout-review`. Do not treat a visual pass, zero pad opens, or a successful upload as final manufacturing validation.

The [recorded workflow guide](docs/recorded-workflow.md) covers preserving connectivity evidence, layout review, assembly placement corrections, and stopping before order submission.

## Safety and evidence

- Edit the authoritative source or generator, not only its output.
- Preserve and compare `schematic-connectivity-v1` when exact connectivity is
  available; label PDF/image-only conclusions visually guided.
- Render and inspect every schematic sheet, dense region, PCB side, and critical
  placement. ERC/DRC cannot replace visual review.
- Treat every unexplained signal or power disconnect as real. Zero pad opens is
  not a release gate by itself.
- Use current primary sources for datasheets, manufacturer guidance, stock,
  pricing, and fabrication capabilities.
- Correct CPL rotation/origin errors in the source mapping, regenerate hashes,
  and re-upload. Browser-only fixes are never manufacturing evidence.
- Keep design-critical substitution, assembly placement, final price, and
  payment approvals separate.

## Real project evidence

The [nescart case study](docs/case-study-nescart.md) records the workflow that
formed these skills: netlist-shaped KiCad pages became visibly wired functional
schematics; architecture informed placement; layer/plane choices and routing
experiments were measured; zero opens was checked against real DRC and power
connectivity; fabrication cost feedback changed via strategy; and every CPL
offset/rotation was corrected and visually rechecked.

![Animated real nescart schematic before/after](assets/case-studies/nescart/schematic-before-after.gif)

## Contributing, support, and license

Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening an issue or pull request.
Usage and evidence requirements are in [SUPPORT.md](SUPPORT.md).

Code and original documentation are [MIT](LICENSE). Real nescart-derived
case-study and banner assets are [CC BY-SA 4.0 with attribution](ASSET-LICENSES.md).
