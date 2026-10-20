# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.45 F1
for `experience` because that label can be confused with `help_request` when a
runner describes a personal situation before asking for advice"*. A reason
that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a uniform random guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

Overall accuracy is at least **0.65 in each of the three seed runs** on the held-out test set.

**Why this target:** I want it to get more than just over half the running posts right for this to feel useful. Some posts mix personal training experience with a question or analysis, so I don't expect it to be right every time.

---

## 2.

Macro F1 is at least **0.60 in each of the three seed runs** on the held-out test set.

**Why this target:** I don't want a good score on the most common label to hide bad results on the others. I picked 0.60 because all three labels should be doing reasonably well, even if a runner's personal story and request for training advice appear in the same post.

---

## 3.

The F1 score for each of `analysis`, `experience`, and `help_request` is at least **0.45 in each of the three seed runs** on the held-out test set.

**Why this target:** I set this lower than the overall target because each label has fewer examples in the test set, so its score can jump around more. `experience` and `help_request` can also look alike when a runner describes training history before asking what to do next.

---

## 4.

In the labelled dataset, no label has more than **50%** of the posts, and every label has at least **20%**.

**Why this target:** I want enough posts in every label for the model to learn from them, and I don't want one label to make up most of the dataset. I chose 20% and 50% to leave room for some kinds of posts to be more common without letting the others get squeezed out.

---

## 5.

In each of the three seed runs, accuracy on the most-confident third of held-out predictions is at least **0.10 higher** than accuracy on the least-confident third.

**Why this target:** I expect the model to be more accurate when it's sure than when it's unsure, especially for clear training questions or posts that evaluate running methods with evidence. I picked a 10-point gap because a tiny difference wouldn't tell me much.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
