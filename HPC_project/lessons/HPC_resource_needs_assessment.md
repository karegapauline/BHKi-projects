### **Lesson: *"What Do I Need? Estimating Computational Resources for Bioinformatics"***

**Half-day (3h)** 

---

#### **Before the lesson — Instructor setup**

**Prerequisites:** Basic familiarity with biological sequencing data. No command line experience required.

---

### **Episode 1 — Why the Request Fails (30 min)**

**Objective:** Learners understand what a resource request is, why vague ones fail, and what information is actually needed — before learning to estimate anything.

**Opening (10 min) — The two-room problem**

Amara is a master's student at University of Ghana. She has 40 blood samples sequenced for her malaria resistance study. She emails the WACCBIP HPC admin: *"Hi, I need an account to run my analysis."*

The admin, Kofi, receives 12 emails like this per week. He doesn't know what Amara's analysis is. He doesn't know if she needs 8 GB or 800 GB of storage. He doesn't know if her job will take 20 minutes or 20 days. He cannot help her without more information — but Amara doesn't know what information to give.

**Discussion (5 min):** What does Kofi need to know? 

**Teach (10 min) — The four things every HPC needs to know**

Introduce the four dimensions. Use the desk/filing cabinet analogy for RAM vs. storage immediately.

| What the system needs to know | What it's called | Analogy |
| ----- | ----- | ----- |
| How many processors does your job use? | **CPU cores** | Number of people working on a task simultaneously |
| How much working memory does it need at peak? | **RAM** | The size of your desk — what you're actively working on |
| How much disk space will your files take? | **Storage** | The filing cabinet — what you keep but aren't using right now |
| How long will it run? | **Walltime** | The deadline you give yourself before stopping |

**{**The RAM vs. storage confusion is the most common misconception in this lesson. Spend time here. A useful check: ask a learner "if your laptop has 8 GB RAM and 256 GB storage, which one fills up when you have too many browser tabs open?" (RAM.) "Which one fills up when you download too many videos?" (Storage.)}

**Formative assessment — Exercise 1.1 (5 min):**

Kofi receives these two requests. Which one can he act on immediately? What's missing from the other?

**Request A:** "I need to run GATK HaplotypeCaller on 20 whole-genome sequenced *P. falciparum* samples. Each sample is about 2 GB of FASTQ data. I expect to need about 32 GB RAM and 200 GB of storage for intermediates. The pipeline should finish in about 3 days."

**Request B:** "I need to run my bioinformatics pipeline on some malaria samples."

---

### **Episode 2 — Reading Your Experiment (60 min)**

**Objective:** Learners translate their own experimental design into resource estimates using a structured method and worked archetypes.

**Teach (15 min) — From biology to compute: the five questions**

Every bioinformatics project can be estimated by answering five questions in order:

1. **What organism?** → genome size → sets RAM and storage floor  
2. **What sequencing technology and depth?** → sets file size per sample  
3. **How many samples?** → multiplies everything  
4. **What is the analysis goal?** → determines which tools and which step is the bottleneck  
5. **One-time run or repeated pipeline?** → determines whether you need long-term storage allocation

Walk through each question using the *P. falciparum* WGS example. Write numbers on the board as you go — don't just say them.

*P. falciparum* genome: 23 Mb. Tiny. But 50x coverage Illumina WGS \= \~1.5 GB FASTQ per sample. 40 samples \= 60 GB raw data. Intermediates (BAM files, GVCFs) \= roughly 3× \= **\~180 GB total storage.** Peak RAM for GATK variant calling \= **32 GB per sample.** Walltime per sample \= **\~10 hours.** Running 8 samples in parallel on 8 nodes \= **\~10 hours total walltime** if you have the nodes.

**Teach (10 min) — The reference table**

Present the archetype table for the four core genomics workflows (variant calling, RNA-seq, 16S microbiome, bacterial genome assembly). Emphasise two things:

* These are **estimates, not guarantees.** The actual numbers depend on the system, the tool version, and the data.  
* The **bottleneck column is the most important column.** It tells you which step to worry about.

Give learners a printed copy — this is a reference they keep, not something they memorise.

**Formative assessment — Exercise 2.1 (20 min):**

Fatoumata is a PhD student at University of Nairobi. Her project: gut microbiome study comparing HIV-positive and HIV-negative individuals in Western Kenya. 120 stool samples, 16S V4 region, Illumina MiSeq.

Using the reference table and the five questions:

1. What is the bottleneck step and why?  
2. Estimate total storage needed.  
3. What is the minimum RAM you must request for that bottleneck step?  
4. Write one sentence describing the peak resource requirement that Fatoumata should put in her request.

**Worked answer (instructor reveals after learners attempt):**

1. DADA2 denoising — loads all 120 samples into RAM simultaneously  
2. 120 × \~400 MB raw × 3 \= \~144 GB storage  
3. 64 GB minimum, 128 GB recommended for 120 samples  
4. *"The DADA2 denoising step requires a high-memory node with at least 64 GB RAM; 128 GB is preferred for 120 samples."*

**Instructor note for mixed groups:** If an administrator is in the room, ask them at this point: "Did you know DADA2 worked this way? Would a request saying 'I need to run QIIME2' have told you this?" This surfaces the knowledge gap from both sides without blame.

**Exercise 2.2 — Your own project (15 min):**

Learners apply the five questions to their own research project. If they don't have one, use a project from the provided list:

* Pan-genome analysis of 60 *Klebsiella* isolates from Kenyan hospitals (AMR surveillance)  
* RNA-seq of cassava infected with cassava mosaic virus, 18 samples (3 conditions × 6 replicates)  
* WGS population structure of tsetse fly (*Glossina fuscipes*) from 5 sites in Uganda, 80 samples

Each learner fills in a simple table: organism / genome size / samples / bottleneck step / peak RAM / total storage / estimated walltime. This becomes the input for Episode 3\.

---

### **Episode 3 — Writing the Request (45 min)**

**Objective:** Learners convert their estimates into a structured, actionable resource request and understand what happens to it on the other side.

**Teach (10 min) — What the admin does with your request**

This section is taught from the administrator's perspective. If an admin is present, let them speak. If not, the instructor takes their role.

Explain what SLURM does with a job submission: it queues the job, waits for the requested resources to be free simultaneously, then starts it. Three things kill jobs before they finish:

* **Out of memory (OOM):** job requested 16 GB, needed 32 GB → killed without warning  
* **Walltime exceeded:** job requested 24h, ran 25h → killed at the 24h mark, all progress potentially lost  
* **Storage full:** job wrote 500 GB into a 200 GB quota → fatal write error, corrupted output

**Instructor note:** These are the three failure modes researchers encounter most. Each one has a solution that comes from the estimation work in Episode 2\. Make the connection explicit: "If you estimated correctly in Episode 2, none of these will happen to you."

**Teach (5 min) — The structure of a good request**

A complete resource request has five parts:

1. One sentence of biological context  
2. The pipeline steps and tools  
3. The peak resource requirement for each step  
4. The total footprint (storage, total walltime window)  
5. Timeline (when does the project start and end)

This maps directly onto the CRMP template. If learners have the CRMP in front of them, point to each section.

**Exercise 3.1 — Rewrite the request (10 min):**

Return to Amara's email from Episode 1\. Now that learners have estimated resources for the *P. falciparum* WGS archetype, rewrite her email as a proper request. Compare in pairs.

**Exercise 3.2 — Role play (15 min, paired):**

One person plays researcher, one plays HPC administrator. The researcher describes their project from Exercise 2.2 verbally. The administrator asks questions until they have everything they need. Then swap.

Debrief: What did the researcher not think to say? What did the admin not know to ask? Write these on the board. These become the basis for the lesson's **common misconceptions** section.

**Instructor note:** This exercise consistently reveals two things: researchers don't know about walltime limits until asked, and administrators don't know that DADA2 behaves differently from other QIIME2 steps. Both are things the lesson has now taught. Naming this in the debrief makes the learning visible.

**Teach (5 min) — What to do after your first job runs**

This is where the external resources enter — but as tools for the next step, not for this lesson:

"After your first job runs, you'll want to check whether you estimated correctly. ILRI and Strathmore HPC both use SLURM. After a job completes, the command `seff <job_id>` tells you how much CPU and memory your job actually used. If you requested 32 GB and used 8 GB, you over-requested — reduce it next time. The Sheffield HPC documentation explains how to read this output in detail \[link\]. If you're writing a formal allocation request for a larger project or a grant, the NCAR documentation shows how to format a core-hours table \[link\]. The Oxford RSE materials cover scalability testing — understanding whether adding more cores actually speeds up your specific tool \[link\]."

The three resources are introduced here as **next steps**, not prerequisites. Learners leave knowing they exist and why they matter, without needing to have read them.

---

### **Wrap-up (15 min)**

**Key takeaways — ask learners to supply, not tell them:**

* What are the four things an HPC admin needs to know?  
* What is the bottleneck step in a 16S microbiome analysis?  
* What happens if your job exceeds its memory request?

**The lesson in one sentence:**

Your experimental design already contains your resource requirements — this lesson taught you how to read them.

**What to do next:**

| If you are a researcher | If you are an administrator |
| ----- | ----- |
| Fill in the CRMP template before your next HPC request | Use the archetype tables as benchmarks when reviewing requests |
| After your first job, run `<job_id>` to check your estimates | Flag incomplete requests with the list of five things from Episode 1, not just "insufficient information" |

---

