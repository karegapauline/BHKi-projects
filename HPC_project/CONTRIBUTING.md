# Contributing to HPC Co-Design for Africa

Thank you for contributing. This project is built on the principle that the people closest to the problem — researchers working with African biological data, and administrators running African HPC systems — are the ones best placed to improve these materials. Every contribution, large or small, makes the tools more useful and more grounded in reality.

---

## What We Need Most

These are the highest-priority gaps right now:

- **Lesson on determining the resources one needs** - We aim to collaborate with HPC users and administrators in this to ensure materials are correct. Feel free to reach out for this.
- **New project archetypes** — workflows not yet in `africa_hpc_projects.csv` (see the list of organisms and methods we know are missing in the database README)
- **Corrections to resource estimates** — if you have run one of the existing archetypes and the CPU/RAM/walltime figures were wrong for your system, please tell us
- **Admin and researcher plain-English descriptions** — if the `admin_plain_english` or `researcher_plain_english` fields in the database don't make sense to the audience they're written for, open an issue
- **New HPC systems** — if you know of an HPC system in Africa not in `data/hpc_systems_africa.csv`, add it
- **Translation and localisation** — if you have adapted materials for a specific country or institution context, we would like to know

---

## Ways to Contribute

### You don't need to use GitHub to contribute

If GitHub is unfamiliar or inaccessible, you can contribute by:

- Emailing Pauline directly at [bioinformaticshubofkenya@gmail.com] with your suggested addition or correction
- Filling in the [contribution form — link TBC] with your suggested new project archetype
- Commenting on the shared Google Doc [link TBC] during open review periods

We will integrate your contribution and credit you in the changelog.

### If you use GitHub

We use a standard fork-and-pull-request workflow. The steps are:

1. Fork the repository
2. Create a branch named for your contribution: `add-cowpea-archetype` or `fix-dada2-ram-estimate` or `add-lesson-plan`
3. Make your changes
4. Open a pull request with a short description of what you changed and why
5. A maintainer will review within two weeks

---

## Adding a New Project Archetype to the Database

This is the most valuable contribution you can make. Before you start:

- Check `data/africa_hpc_projects.csv` to confirm the project type is not already there
- Run the scraper notebook (`notebooks/03_africa_projects_scraper.ipynb`) to see if it surfaces relevant literature you can use as a source

### Required fields

Every new row in `africa_hpc_projects.csv` must include:

| Field | What it should contain |
|---|---|
| `project_id` | Next P0XX number in sequence |
| `research_area` | One of: crop genomics / malaria research / vector biology / infectious disease / human health genomics / microbiome / livestock genomics — or propose a new category |
| `organism` | Scientific name |
| `common_name` | Plain English name |
| `project_type` | Short label (e.g. "SNP discovery and GWAS") |
| `project_description` | One or two sentences |
| `africa_context` | Why this project matters in an African research context specifically |
| `admin_plain_english` | Explanation of the project for an HPC admin with no biology background — test it on someone who fits that description if possible |
| `researcher_plain_english` | Explanation of the compute requirements for a researcher with no HPC background — same test applies |
| `bottleneck_step` | Which pipeline step is the limiting factor |
| `bottleneck_reason` | Why — in plain terms |
| `notes` | Any organism-specific quirks, known pitfalls, or things to confirm with the researcher before allocating resources |

### Fields that can be approximate

The resource fields (CPU, RAM, walltime) are estimates, not guarantees. It is better to have a rough, clearly-labelled estimate than no entry. Use the archetype tables in the lesson as a cross-check, and note in `notes` if your figures come from a specific system configuration.

### Source requirement

Every new archetype should cite at least one published paper or dataset that supports the workflow and resource estimates. Add the citation to the `publicly_available_datasets` or `notes` field.

---

## Correcting Existing Resource Estimates

If you have run a pipeline from the database on a real African HPC system and the figures were meaningfully different from what is listed:

1. Open an issue with the label `resource-correction`
2. Include: the project ID, the step that was wrong, what the figures actually were, and which system you ran it on (institution and approximate specs)
3. If the difference is large (e.g. DADA2 needing 256 GB not 64 GB for your sample size) please say so clearly — these corrections help administrators avoid under-allocating

We do not need exact reproducibility. What matters is that the estimates are useful as a starting point for the communities using them.

---

## Adding an HPC System to the Infrastructure Map

Open `data/hpc_systems_africa.csv` and add a row with:

- System name
- Institution
- Country
- City (for mapping)
- Approximate number of cores (if known publicly)
- RAM per node (if known publicly)
- Primary user community (bioinformatics / physics / general research / etc.)
- Access model (institutional / project-based / open application / etc.)
- Contact or URL for access requests (if public)

If you are not sure of some fields, leave them blank — a partial entry is better than no entry. Do not include any information that the institution has not made public.

---

## Reviewing the Lesson Materials

The Carpentries-style lesson in `lessons/01_resource-needs-assessment/` is in not yet an active draft. You can contribute by:

- Helping create a draft of what would be useful
- Suggesting new exercises
- Flagging language that does not make sense to a biologist, or to an administrator, depending on which hat you wear

If you run a workshop using these materials, we would love to hear how it went. Open an issue with the label `workshop-report` and describe: audience, institution, what worked, what did not.

---

## Style and Tone Guidelines

These apply to all contributions to lesson text, database descriptions, and documentation:

**The two plain-English fields are the most important thing to get right.** The `admin_plain_english` field should be readable by someone who manages servers and has never heard of GATK. The `researcher_plain_english` field should be readable by a biology MSc student who has never submitted a job to a scheduler. If you are not sure whether you have got this right, ask a colleague who fits that description to read it.

**Avoid jargon without explanation.** Acronyms should be expanded on first use. Tool names can appear without explanation but should be accompanied by what the tool does (e.g. "BWA-MEM2, which aligns DNA reads to a reference genome").

**Be specific about Africa.** Generic bioinformatics advice exists in abundance. What is valuable here is grounding in African institutions, organisms, and research contexts. Mention specific institutions, datasets, and collaborators where you can.

**Estimates over omissions.** A rough estimate with a note that it is approximate is always more useful than leaving a field blank.

---

## Code of Conduct

This project follows the [Carpentries Code of Conduct](https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html). In summary: be respectful, assume good faith, and prioritise the learning and safety of community members who are newer to this work. Contributions from researchers and administrators at all career stages and from all African institutions are equally welcome.

---

## Credit and Attribution

All contributors will be acknowledged in the project's `CONTRIBUTORS.md` file and in any publications arising from this work. If you contributed to a specific output (a new archetype, a lesson exercise, a workshop report), that contribution will be noted specifically.

This project is shared under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). By contributing, you agree that your contributions may be shared and adapted under the same licence, with attribution.

---

## Questions

Not sure whether something counts as a contribution, or how to get started? Open an issue with the label `question` or email [email]. There are no silly questions here — the project exists precisely because not everyone starts with the same background knowledge.
