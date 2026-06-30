# HPC Co-Design for Africa

**Bridging the gap between biological research and high-performance computing in East and West Africa.**

This repository contains open training materials, templates, and tools developed through the HPC Co-Design project — a collaboration led by the [Bioinformatics Hub of Kenya (BHKi)](https://www.bioinfohubke.com/) to improve access to and use of HPC resources across African research institutions.

---

## The Problem

High-performance computing infrastructure exists across Africa — but it is consistently underused. The barriers are not primarily technical. They are:

- Researchers who do not know how to assess or articulate their computational needs
- HPC administrators who have resources but they are underutilized
- No shared language between the two groups
- Training curricula that jump from introductory to advanced, skipping the practical middle ground

This project co-designs the tools, language, and training to fill that gap — with and for the communities who need it.

---

## What's in This Repository

```
hpc-codesign-africa/
├── lessons/
│   └── 01_resource-needs-assessment/   ← Carpentries-style lesson: estimating compute needs (no draft yet)
├── templates/
│   └── computational-resource-plan/    ← DMP-style shared form for researchers + admins
├── data/
│   └── hpc_systems_africa.csv          ← Inventory of HPC systems across Africa
├── notebooks/
│   └── 01_literature_search.ipynb      ← Systematic literature review pipeline
│   └── 02_hpc_mapping.ipynb            ← Geospatial mapping of HPC infrastructure
├── outputs/
│   └── figures/                        ← Maps and visualisations
└── docs/
    └── proposal_draft.md               ← Project proposal (working draft)
```

---

## Outputs

### 📘 Lesson 1: Knowing What You Need
*A Carpentries-style lesson for biology researchers and HPC administrators*

Teaches researchers how to translate their experimental design into a computational resource estimate — and teaches administrators what questions to ask. Covers:
- The four dimensions of compute: CPU, RAM, storage, walltime
- Some genomics workflow archetypes with full resource profiles (variant calling, RNA-seq, microbiome, genome assembly)
- Exercises for mixed researcher–administrator audiences

→ [`lessons/01_resource-needs-assessment/`](lessons/01_resource-needs-assessment/)

---

### 📋 Template: Computational Resource Management Plan (CRMP)
*A shared DMP-style form that bridges researcher needs and administrator allocation*

A structured short document that travels with a project from initial request through completion. Designed to be filled in collaboratively by researcher and HPC administrator.

→ [`HPC_project/templates/CRMP_template.docx`](CRMP_template.docx)

---

### 🗺️ HPC Infrastructure Map
*Geospatial inventory of HPC systems across Africa*

An interactive map of known HPC systems in Africa, with metadata on operator, capacity, primary user community, and access model.

→ [`notebooks/02_hpc_mapping.ipynb`](notebooks/02_hpc_mapping.ipynb) | [View map](#) *(link to website/GitHub Pages)*

---

## Who This Is For

| Audience | What's useful |
|---|---|
| **Biology researchers new to HPC** | Lesson 1, the CRMP template |
| **HPC administrators** | Lesson 1 (admin perspective), archetype reference tables |
| **Trainers and educators** | Full lesson plans with instructor notes, exercises, timing |
| **Research institutions** | CRMP template for onboarding workflows |
| **Funders and collaborators** | Project proposal, infrastructure data |

---

## Project Context

This work is part of a co-design study examining how African research communities can better access and utilise existing HPC infrastructure, with a focus on a Kenya–West Africa pilot. The project is community-led, with BHKi acting as the steering entity in collaboration with partner institutions across the region.

The co-design approach means that tools and materials in this repository are developed with input from both researchers and administrators at African institutions — not designed externally and delivered to them.

A full description of the project, methodology, and findings is available at: **[project website — link TBC]**

---

## Status

| Output | Status |
|---|---|
| Lesson 1: Resource needs assessment | 🔴 Coming soon |
| CRMP template | 🟡 Draft — open for review |
| HPC systems data | 🟡 Partial — contributions welcome |
| Literature review notebook | 🟢 Complete |
| HPC mapping notebook | 🟡 In progress |
| Project website | 🔴 Coming soon |

---

## Contributing

We welcome contributions from HPC administrators, bioinformatics trainers, and researchers across Africa. Ways to contribute:

- **Add an HPC system** — if you know of a system not in our dataset, open an issue or submit a PR to `data/hpc_systems_africa.csv`
- **Review the lesson** — try it with your community and open an issue with feedback
- **Adapt the CRMP** — if your institution has adapted the template, we would like to hear how
- **Share your archetype** — if your workflow is not covered by the four archetypes in Lesson 1, consider contributing a new one
- **Offer HPC space** - if you are an administrator, help us grow this community being the resource holder

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## Citation

If you use these materials, please cite:

> Karega P. et al. (2025). *HPC Co-Design for Africa: Training materials and tools.* Bioinformatics Hub of Kenya (BHKi). GitHub: https://github.com/karegapauline/BHKi-projects/HPC_project

---

## Licence

All materials in this repository are shared under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) unless otherwise noted. You are free to adapt and reuse with attribution.

---

## Contact

**Pauline Karega** — BHKi, Kenya
[GitHub](https://github.com/karegapauline) | [bioinformaticshubofkenya@gmail.com]

*This project is affiliated with the Bioinformatics Hub of Kenya (BHKi) and conducted in collaboration with partner institutions in East and West Africa.*
