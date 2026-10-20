# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

This classifier sorts public posts from [r/cybersecurity](https://www.reddit.com/r/cybersecurity/) by their primary communicative purpose. `analysis` posts explain or evaluate a cybersecurity issue using concrete, checkable details; `experience` posts mainly recount the author's own work or learning without primarily asking for help or making an evidence-backed analysis; `help_request` posts explicitly ask readers for advice or information. The labels describe what a post is doing, not whether its author or opinion is right.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** The post's main purpose is to explain or evaluate a cybersecurity issue, supported by concrete, checkable details such as a source, timeline, measurement, or observed evidence.

**Example 1:** The post about a five-month Log4Shell campaign against Ukraine's state data-exchange system describes how the exposed directory revealed the operation.
> [Ukraine's state data-exchange system targeted in a 5-month Log4Shell campaign](https://www.reddit.com/r/cybersecurity/comments/1xauvjc/ukraines_state_dataexchange_system_targeted_in_a/)

**Example 2:** The post about ransomware data dumps notes the number and size of posted archives and the absence of a file tree, using those observations to discuss what can responsibly be inferred.
> [100+ 1G files from darkweb - can people really download leaked data?](https://www.reddit.com/r/cybersecurity/comments/1xaxgzg/100_1g_files_from_darkweb_can_people_really/)

### `experience`

**Definition:** The post's main purpose is to recount the author's own cybersecurity work, workplace, or learning, without primarily asking readers for help or using evidence to explain or evaluate a broader issue.

**Example 1:** The author describes their company's global on-call rotation, team size, and weekend coverage.
> [Large Companies - What's your (Cyber) on-call Schedule Like?](https://www.reddit.com/r/cybersecurity/comments/1xav151/large_companies_whats_your_cyber_oncall_schedule/)

**Example 2:** The author says most of their work week goes to compliance spreadsheets and describes the effect on their technical skills.
> [Anyone else feel like they’re just a glorified spreadsheet administrator at this point?](https://www.reddit.com/r/cybersecurity/comments/1xa7x8b/anyone_else_feel_like_theyre_just_a_glorified/)

### `help_request`

**Definition:** The post explicitly asks readers for guidance, recommendations, or information about a cybersecurity task or decision; personal background or supporting facts do not change that purpose.

**Example 1:** A new analyst asks for practical guidance on setting up and testing a mobile app.
> [Guidance for mobile application security testing](https://www.reddit.com/r/cybersecurity/comments/1xay1m4/guidance_for_mobile_application_security_testing/)

**Example 2:** The author asks whether blocking all internet access and allowlisting needed services is worthwhile, and what strategies others use.
> [Blocking the Entire Internet](https://www.reddit.com/r/cybersecurity/comments/1xauxhj/blocking_the_entire_internet/)

### The hardest boundary

**Which two labels:** `experience` and `help_request`

**The decision rule I used every time:**
The borderline post is [“Blocking the Entire Internet”](https://www.reddit.com/r/cybersecurity/comments/1xauxhj/blocking_the_entire_internet/): it describes the author's team's idea, but asks whether it is worthwhile and what strategies others use. First, label an explicit, genuine request for advice or information `help_request`, even if it includes workplace context or evidence. If there is no such request, label a post `analysis` only when it uses concrete, checkable support to explain or evaluate a broader cybersecurity issue; otherwise label a first-person account `experience`. A rhetorical question that does not actually seek a response does not count as a help request.


---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

**Counts per label:**

| Label | Count | Share |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**2.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**3.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* I gave the three label definitions to an AI tool and asked it to write eight fictional cybersecurity posts that stress-test the boundaries.
- *What came back:* Eight short, fictional cases. I classified each using the decision rule:
  1. “I now handle the weekly access-review rota. It takes two hours, but the handoff is smoother than last quarter.” — `experience`: a personal account without a request or broader evidence-based evaluation.
  2. “I inherited the weekly access-review rota and keep missing exceptions. How do other teams track them?” — `help_request`: explicitly asks for advice, despite its personal context.
  3. “I reviewed 120 access alerts over four weeks; 31 were duplicates, and removing them cut the queue by about a quarter.” — `analysis`: uses a measurable observation to evaluate a broader workflow issue.
  4. “For four weeks I helped review access alerts. The repetitive queue was the hardest part of my rotation.” — `experience`: first-person account, with no request or supported broader claim.
  5. “Our new MFA prompt confused several staff in my first week supporting it. What wording has helped other teams explain a change like this?” — `help_request`: asks for a recommendation; the work anecdote is context.
  6. “The incident report gives a disclosure date, affected service, and confirmed record count; those details make the scope clearer than the initial notice.” — `analysis`: evaluates a public issue using checkable details.
  7. “I moved from IT support into a junior security role this year. Which fundamentals helped you most in your first six months?” — `help_request`: explicitly requests information, although most of the post is personal background.
  8. “During my first month on call, I escalated two alerts that turned out to be benign. Writing down why helped me recognize the same pattern later.” — `experience`: recounts personal learning without requesting help or making a broader evidence-backed evaluation.
- *What I changed:* I made the priority explicit: a genuine request for advice or information is `help_request`; absent a request, concrete evidence used to explain or evaluate a broader issue is `analysis`; otherwise, a first-person account is `experience`. I also clarified that a rhetorical question alone is not a request.

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:** No dataset posts have been pre-labelled. The eight AI-generated posts above were only a taxonomy stress test and are not part of the dataset.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
