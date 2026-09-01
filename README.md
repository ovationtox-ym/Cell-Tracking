# Cell Tracking During Development

Work log for the Kaggle competition [Biohub - Cell Tracking During Development](https://www.kaggle.com/competitions/biohub-cell-tracking-during-development).

This is a personal learning project. The aim is to understand the pipeline end to end, not to place on the leaderboard.

## Problem

Given 3D+time light-sheet microscopy recordings of zebrafish embryos, detect cells and link them across time to reconstruct lineages.

The task splits into two stages:

1. **Detection** — locate cell centers in each timepoint
2. **Linking** — connect nodes between `t` and `t+1`. A node that splits into two is a division.

## Submission format

A single CSV holds two kinds of rows, distinguished by `row_type`.

| row_type | Columns used | Meaning |
|---|---|---|
| `node` | node_id, t, z, y, x | Position of a detected cell |
| `edge` | source_id, target_id | Two nodes are the same cell |

- Unused columns are filled with `-1`
- `node_id` is assigned by the submitter and only needs to be unique within a dataset
- Divisions have no row of their own. **A source_id appearing in two edges is a division.**

## Evaluation

Micro-averaged Jaccard over edges and over divisions, combined.

Since divisions account for half the score, any approach that only produces one-to-one matches between consecutive frames is structurally incapable of scoring on that half.

## Goals

- [ ] Reproduce the royerlab baseline
- [ ] Complete a full submission (code competition, inference runs offline)
- [ ] Test one hypothesis

## Setup

- WSL2 Ubuntu, Python venv
- Training on a remote GPU (TBD); inference in a Kaggle notebook
- Data (~88 GB) and model weights are not committed — see `.gitignore`

## References

- [royerlab baseline](https://github.com/royerlab/kaggle-cell-tracking-competition)

## Log

- 2026-08-25 — Environment setup; analyzed submission format
