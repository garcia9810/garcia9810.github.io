---
name: NFL Fourth-Down Conversion Model
tools: [Python, scikit-learn, Pandas, nflreadpy, Matplotlib]
image: assets/pngs/final_project_scshot.png
description: Random forest classifier that estimates the probability an NFL fourth-down attempt is converted, trained on nflverse play-by-play data and evaluated on a held-out season.
---

# NFL Fourth-Down Conversion Model

A machine learning project that predicts the probability of converting a fourth down from the
game state at the snap — distance to go, field position, play call, and the teams on the field —
using NFL play-by-play data.

<p class="text-center">
{% include elements/button.html link="https://github.com/garcia9810/Final_Project_Football" text="View on GitHub" %}
</p>

![Calibration curve and predicted probability distribution for the fourth-down model](/assets/pngs/final_project_scshot.png)

## The Question

Fourth down is the highest-leverage decision in football: go for it, punt, or kick. Answering that
well starts with a single number — how likely is this attempt to succeed? This project builds a
model for exactly that number and checks whether the probabilities it produces can be trusted.

## Data

Play-by-play data comes from the nflverse project via `nflreadpy`, filtered to fourth-down
attempts. The most recent season is held out as the test set, with prior seasons used for
training — 4,437 training plays and 116 test plays. Roughly 52.9% of training attempts were
converted, so the classes are close to balanced.

## Features

- **togo** — yards to the first-down marker (1–34)
- **yardline** — yards from the opponent's end zone (1–99)
- **play_type** — pass or run
- **posteam** / **defteam** — offense and defense

Numeric features pass through unscaled, `play_type` is one-hot encoded, and the two team columns
are target encoded — each abbreviation is replaced with that team's conversion rate in the
training data — so 32 teams become one numeric column apiece instead of a wide sparse block.

## Model and Tuning

A scikit-learn pipeline wraps the preprocessing and a random forest classifier. `GridSearchCV`
with 5-fold cross-validation searched `n_estimators`, `max_depth`, and `min_samples_leaf`, scoring
on negative log loss rather than accuracy — the goal is a calibrated probability, not a hard
yes/no call. The best configuration was 300 trees with `max_depth=5` and `min_samples_leaf=10`,
at a cross-validated log loss of 0.6439.

## Results

On the held-out season the tuned model reached a **log loss of 0.5810** and a **ROC-AUC of
0.7697** — it improved on its own cross-validation loss and ranks converted plays above failed
ones far better than chance.

The calibration curve above is the more interesting plot. Across the range where the model
actually makes predictions it tracks the diagonal closely, meaning a stated 70% really does
convert about 70% of the time. The companion histogram shows why: converted and unconverted
plays separate, but they overlap heavily in the middle — the model is honest about the fourth
downs that genuinely are coin flips.

## What the Model Learned

Conversion rate falls steeply as yards-to-go increases, and run plays convert at a higher rate
than pass plays — the two dominant signals, and both match how fourth-down decisions are
discussed in practice. Because the output is a calibrated probability rather than a label, it
slots directly into the kind of win-probability and decision models NFL teams use to decide
whether to go for it.
