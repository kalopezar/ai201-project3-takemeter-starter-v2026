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

I want to sort public posts from [r/running](https://www.reddit.com/r/running/) by what they are mainly doing. `analysis` means explaining or evaluating a running topic with checkable details, `experience` means describing your own running or training, and `help_request` means asking readers for advice or information. The labels are about the purpose of a post, not whether I agree with it. I still need to read the community posts and make a complete, reviewed dataset before I can train a running classifier.

**My repository:** [https://github.com/kalopezar/ai201-project3-takemeter-starter-v2026](https://github.com/kalopezar/ai201-project3-takemeter-starter-v2026)

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `analysis`

**Definition:** The post's main purpose is to explain or evaluate a running topic, supported by concrete, checkable details such as training data, race results, or a described comparison.

**Example 1 (candidate; read and confirm):** The author reviews a running-plan app after using it for a year and compares its plans and customization.
> [In-depth review of Runna after using it for a year](https://www.reddit.com/r/running/comments/1tfyl2u/indepth_review_of_runna_after_using_it_for_a_year/)

**Example 2 (candidate; title only, read and confirm):** The title raises whether Zone 2 training is necessary or overhyped; check the full post before deciding it is analysis rather than a request for opinions.
> [Do I actually need to run Zone 2 or is it overhyped?](https://www.reddit.com/r/running/comments/1suhptl/do_i_actually_need_to_run_zone_2_or_is_it/)

### `experience`

**Definition:** The post's main purpose is to recount the author's own running, training, or race experience, without primarily asking readers for advice or evaluating a broader training question with evidence.

**Example 1 (candidate; read and confirm):** The author recounts personal experience using a training-plan app over two training blocks; decide whether the review is mainly personal experience or evidence-backed analysis.
> [In-depth review of Runna after using it for a year](https://www.reddit.com/r/running/comments/1tfyl2u/indepth_review_of_runna_after_using_it_for_a_year/)

**Example 2 (candidate; read and confirm):** The author describes starting to run later in life and their training progress, but also asks readers several questions, so the decision rule may put it under `help_request`.
> [Started running at 39. For those who also started later — what happened to your fitness in years 2–4?](https://www.reddit.com/r/running/comments/1w4c85u/started_running_at_39_for_those_who_also_started/)

### `help_request`

**Definition:** The post explicitly asks readers for guidance, recommendations, or information about running or a training decision; personal background or supporting facts do not change that purpose.

**Example 1 (candidate; read and confirm):** A runner asks peers how fitness and durability changed after starting to run later in life.
> [Started running at 39. For those who also started later — what happened to your fitness in years 2–4?](https://www.reddit.com/r/running/comments/1w4c85u/started_running_at_39_for_those_who_also_started/)

**Example 2 (candidate; title only, read and confirm):** A beginner Q&A thread is intended for questions from new runners.
> [New to running or the sub? Click here first!](https://www.reddit.com/r/running/comments/1qtznm4/new_to_running_or_the_sub_click_here_first/)

### The hardest boundary

**Which two labels:** `experience` and `help_request`

**The decision rule I used every time:**
The borderline post is [“Started running at 39. For those who also started later — what happened to your fitness in years 2–4?”](https://www.reddit.com/r/running/comments/1w4c85u/started_running_at_39_for_those_who_also_started/): it contains a detailed personal training story but explicitly asks readers about their experience. Between `experience` and `help_request`, label a post `help_request` when it genuinely asks readers for advice or information, even if most of the text is personal background. Label it `experience` when it mainly recounts the author's own running without asking for guidance. If there is no genuine request, use `analysis` only when concrete details support an explanation or evaluation of a broader running topic. A rhetorical question that does not seek a response is not a help request. This is a provisional decision from the available post summary; confirm it after reading the full post.


---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** The training dataset is 200 original synthetic running posts generated for this exercise. They are not Reddit posts and do not represent the [r/running](https://www.reddit.com/r/running/) community. `data/running_source_manifest.csv` contains separate public-post candidates; I have not completed the required 30–40-post community reading.

**How I labelled them:** All 200 synthetic examples were generated and assigned labels with AI assistance. None are cold labels, user-reviewed community posts, or full-text posts collected from Reddit. The nine rows in the source manifest are only title/snippet-based suggestions and are not included in the training data.

**Dataset file:** `labels.csv` contains the 200 synthetic training examples. Each row's note identifies it as AI-generated, synthetic, not a real community post, and not cold-labeled.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| `analysis` | 67 | 33.5% |
| `experience` | 67 | 33.5% |
| `help_request` | 66 | 33.0% |
| **Total** | **200 synthetic examples** | **100%** |

**Progress:** The requested 200-row training file is complete as a synthetic demonstration. It does not satisfy the real-community post collection or personal reading requirement; I have not read 30–40 posts for the required 20 minutes, and the real-community dataset remains 0 reviewed examples.

**Training caveat:** Training below uses synthetic examples only. Its metrics describe how the model learned these generated examples and must not be reported as performance on real running-community posts. The source manifest remains a separate, unreviewed list of candidates.

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

<!-- Provisional AI-assisted candidates from the source manifest below; read
     each full post and replace or confirm these with cases that made you pause. -->

**1.**
> *The post:* [“In-depth review of Runna after using it for a year”](https://www.reddit.com/r/running/comments/1tfyl2u/indepth_review_of_runna_after_using_it_for_a_year/) — a first-person review of a training app based on two training periods.
>
> *Could have been:* `experience` or `analysis`
>
> *AI-assisted provisional choice:* `analysis`, if the full post's main purpose is to evaluate the app using comparisons and concrete training details; use `experience` if it mainly recounts the author's personal use. Read the full post before confirming.

**2.**
> *The post:* [“Started running at 39. For those who also started later — what happened to your fitness in years 2–4?”](https://www.reddit.com/r/running/comments/1w4c85u/started_running_at_39_for_those_who_also_started/) — describes the author's training and asks others how their fitness changed over time.
>
> *Could have been:* `experience` or `help_request`
>
> *AI-assisted provisional choice:* `help_request`, because the author explicitly asks other runners questions; the personal training details are context for the request.

**3.**
> *The post:* [“Do I actually need to run Zone 2 or is it overhyped?”](https://www.reddit.com/r/running/comments/1suhptl/do_i_actually_need_to_run_zone_2_or_is_it/) — the title asks about a training method, but the full post has not been reviewed.
>
> *Could have been:* `analysis` or `help_request`
>
> *AI-assisted provisional choice:* `help_request` if the author is seeking other runners' advice; use `analysis` if the post mainly evaluates the training method with evidence and the question is rhetorical. Read and classify from the full text.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:** `distilbert-base-uncased` (synthetic-data demonstration only)

**Settings:** 3 epochs, learning rate `2e-5`, batch size 16, max length 128, seed 42

**Device:** CPU (`torch 2.14.1+cpu`)

**Anything I changed from the defaults, and why:** No hyperparameters changed. I trained on the 200-row synthetic `labels.csv` because real community posts and personally reviewed labels are not available. This is an end-to-end training demonstration, not a valid evaluation of an r/running classifier.

**Split sizes:** 139 train / 31 validation / 30 test; the test split contains 10 examples of each label.

**Seed 42 test results:** Accuracy 1.00, macro F1 1.00, with F1 1.00 for `analysis`, `experience`, and `help_request`. Most-confident-third accuracy was 1.00 and least-confident-third accuracy was 1.00.

**Interpretation:** The perfect scores reflect the highly regular, AI-generated examples and this small synthetic test split. They are not evidence of real-world accuracy and must not be reported as performance on genuine running-community posts.


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* For the running topic, I asked an AI tool to write eight fictional boundary-test posts and classify them using the three labels.
- *What came back:* Eight short, fictional cases with AI-suggested labels. The examples below illustrate how the written decision rule applies; they are a synthetic taxonomy exercise, not labels from posts I personally read:
  1. “I ran my first 5K last month and now run the same loop twice a week; the routine has made it easier to keep going.” — `experience`: a personal account without a request or broader evidence-based evaluation.
  2. “I keep adding distance and my calves are sore the next day. How many rest days should I take?” — `help_request`: explicitly asks for advice, despite its personal context.
  3. “I compared six weeks of easy runs before and after slowing my pace; my average heart rate fell while the distance stayed similar.” — `analysis`: uses a measurable observation to evaluate a training change.
  4. “My first half marathon was harder than expected, especially the last few kilometres, but finishing felt great.” — `experience`: first-person account, with no request or supported broader claim.
  5. “My easy pace feels almost too slow. What signs do you use to tell whether an easy run is actually easy?” — `help_request`: asks for guidance; the personal context is secondary.
  6. “Across my last ten runs, the hotter afternoons had higher heart rates at the same pace; temperature may be affecting my effort.” — `analysis`: evaluates a pattern using checkable details.
  7. “I started running this year and want to train for a 10K. Which beginner plan worked for you?” — `help_request`: explicitly requests information, although most of the post is personal background.
  8. “During my first trail race I walked the steep climbs and enjoyed the course more than I expected.” — `experience`: recounts personal learning without requesting help or making a broader evidence-backed evaluation.
- *What I changed:* I made the priority explicit: a genuine request for advice or information is `help_request`; absent a request, concrete evidence used to explain or evaluate a broader running topic is `analysis`; otherwise, a first-person account is `experience`. I also clarified that a rhetorical question alone is not a request.

**Moment 2**

- *What I asked for:* I asked an AI tool to create original synthetic running examples for `analysis`, `experience`, and `help_request`, with balanced counts for a local training demonstration.
- *What came back:* A 200-row synthetic dataset with labels assigned during generation.
- *What I changed:* I kept the data explicitly marked as synthetic and not cold-labeled. I did not present any generated text as a Reddit post or as something I personally read.

**Pre-labelling disclosure:** All 200 rows in `labels.csv` are AI-generated synthetic examples with AI-assigned labels; none are cold-labeled or from real community posts. The public-source manifest contains only title/snippet-based candidates and is not part of the training data. The eight fictional posts from Moment 1 are a separate taxonomy stress test.

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
     direction. "7 real help_request posts were called experience and only 3 went the
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
