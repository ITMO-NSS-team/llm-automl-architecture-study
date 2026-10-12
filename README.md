# Architecture over Parameters: How Far Agentic Design Patterns Carry a Weak Model in Automated Machine Learning

Supplementary material for the paper: the execution trace of every trial and
the tables derived from the traces.

The paper separates three parts of an agentic AutoML system: the language
model, the harness around it and the expert instruction file. Three harnesses
run on one open-weight model, `gemma-4-31b-it`: FEDOT.LLM (a fixed-stage
workflow over the FEDOT AutoML library), AutoDS-Tools (six agents) and
Terminus-2 (a single agent with a shell). The benchmarks are TabReD (eight
tabular tasks with eighteen published tuned methods), MLAgentBench (ten tasks
that start from a working script) and three scientific case studies. All runs
execute in the [Harbor](https://github.com/harbor-framework/harbor) framework.

## Contents

| Path | Content |
|---|---|
| [`runs/`](runs) | Harbor job directories: 558 trials in 26 cells, grouped by benchmark, harness and configuration |
| [`result_files/`](result_files) | one table with every trial, per-cell and per-task summaries, the paired statistics, the trace analysis and the text of the instruction file |

A trial is one attempt at one task. A cell is one configuration run over all
tasks of a benchmark, with three attempts per task unless stated.

## Configurations

The paths are relative to `runs/<benchmark>/`. The column "Reported in" refers
to the tables, figures and sections of the paper.

### TabReD (`runs/tabred`)

| Directory | Instruction file | Image | Language model | Parallel trials | Trials | Reported in |
|---|---|---|---|---|---|---|
| [`fedot-llm/library-built-in`](runs/tabred/fedot-llm/library-built-in) | library built in | FEDOT | gemma-4-31b-it | 2 | 28 | Table 3, Fig. 2, Table 6 |
| [`terminus-2/stock-image`](runs/tabred/terminus-2/stock-image) | none | stock | gemma-4-31b-it | 2 | 24 | Table 3, Fig. 2, Table 6 |
| [`terminus-2/enriched-image`](runs/tabred/terminus-2/enriched-image) | none | enriched | gemma-4-31b-it | 2 | 24 | Sections 6.1, 6.3 and 7.1, Fig. 4 |
| [`terminus-2/file-none`](runs/tabred/terminus-2/file-none) | none | enriched | gemma-4-31b-it | 4 | 24 | Table 8, Section 6.4, Fig. 4 |
| [`terminus-2/file-library`](runs/tabred/terminus-2/file-library) | library | enriched | gemma-4-31b-it | 4 | 24 | Table 8, Fig. 4 |
| [`terminus-2/file-discipline`](runs/tabred/terminus-2/file-discipline) | discipline | enriched | gemma-4-31b-it | 4 | 24 | Table 8, Fig. 4 |
| [`terminus-2/file-discipline-trimmed`](runs/tabred/terminus-2/file-discipline-trimmed) | discipline trimmed | enriched | gemma-4-31b-it | 4 | 24 | Table 8, Fig. 4 |
| [`terminus-2/file-both`](runs/tabred/terminus-2/file-both) | both | enriched | gemma-4-31b-it | 4 | 24 | Table 8, Fig. 4 |
| [`terminus-2/model-gemma-4-26b-a4b-it`](runs/tabred/terminus-2/model-gemma-4-26b-a4b-it) | none | enriched | gemma-4-26b-a4b-it | 4 | 24 | Section 6.4, Fig. 4 |
| [`terminus-2/model-glm-4.7`](runs/tabred/terminus-2/model-glm-4.7) | none | enriched | glm-4.7 | 4 | 24 | Section 6.4, Fig. 4 |
| [`autods-tools/file-none`](runs/tabred/autods-tools/file-none) | none | enriched | gemma-4-31b-it | 4 | 24 | Table 7, Fig. 2, Fig. 4, Section 7 |
| [`autods-tools/file-library`](runs/tabred/autods-tools/file-library) | library | enriched | gemma-4-31b-it | 4 | 24 | Table 7, Fig. 4, Section 7 |
| [`autods-tools/file-discipline`](runs/tabred/autods-tools/file-discipline) | discipline | enriched | gemma-4-31b-it | 4 | 24 | Table 7, Fig. 4, Section 7 |
| [`autods-tools/file-both`](runs/tabred/autods-tools/file-both) | both | enriched | gemma-4-31b-it | 4 | 24 | Table 3, Fig. 2, Tables 6 and 7, Fig. 4, Section 7 |
| [`autods-tools/model-gemma-4-26b-a4b-it`](runs/tabred/autods-tools/model-gemma-4-26b-a4b-it) | both | enriched | gemma-4-26b-a4b-it | 4 | 24 | Section 6.4, Fig. 4 |
| [`autods-tools/model-glm-4.7`](runs/tabred/autods-tools/model-glm-4.7) | both | enriched | glm-4.7 | 4 | 24 | Section 6.4, Fig. 4 |

### MLAgentBench (`runs/mlagentbench`)

| Directory | Instruction file | Image | Language model | Parallel trials | Trials | Reported in |
|---|---|---|---|---|---|---|
| [`terminus-2/file-none`](runs/mlagentbench/terminus-2/file-none) | none | stock | gemma-4-31b-it | 4 | 24 | Tables 4 and 6 |
| [`autods-tools/file-none`](runs/mlagentbench/autods-tools/file-none) | none | enriched | gemma-4-31b-it | 4 | 30 | Tables 4 and 6 |
| [`autods-tools/file-both`](runs/mlagentbench/autods-tools/file-both) | both | enriched | gemma-4-31b-it | 4 | 30 | Tables 4 and 6 |
| [`autods-tools/file-none_cifar10-imdb`](runs/mlagentbench/autods-tools/file-none_cifar10-imdb) | none | enriched | gemma-4-31b-it | 2 | 4 | Section 4.5 |

### Case studies (`runs/case-studies`)

| Directory | Task text | Image | Language model | Parallel trials | Trials | Reported in |
|---|---|---|---|---|---|---|
| [`autods-tools/text-with-library-section`](runs/case-studies/autods-tools/text-with-library-section) | with library section | enriched | gemma-4-31b-it | 2 | 9 | Table 5, Fig. 3 |
| [`terminus-2/text-with-library-section`](runs/case-studies/terminus-2/text-with-library-section) | with library section | enriched | gemma-4-31b-it | 4 | 9 | Table 5, Fig. 3 |
| [`terminus-2/text-plain`](runs/case-studies/terminus-2/text-plain) | without library section | enriched | gemma-4-31b-it | 4 | 9 | Table 5, Fig. 3 |
| [`fedot-llm/text-plain`](runs/case-studies/fedot-llm/text-plain) | without library section | FEDOT | gemma-4-31b-it | 4 | 6 | Table 5, Fig. 3 |

### Earlier single-attempt runs (`runs/earlier-single-attempt`)

One attempt at each of the eighteen TabReD and MLAgentBench tasks on an
earlier adaptation of the tasks. The paper uses these two cells only for the
repair-loop counts of Section 7.3.

| Directory | Instruction file | Language model | Trials |
|---|---|---|---|
| [`autods-tools/file-both`](runs/earlier-single-attempt/autods-tools/file-both) | both | gemma-4-31b-it | 18 |
| [`autods-tools/file-none`](runs/earlier-single-attempt/autods-tools/file-none) | none | gemma-4-31b-it | 18 |

Notes on the configurations:

- Instruction file. The file of AutoDS-Tools has a library part and a
  discipline part. `none`, `library`, `discipline` and `both` name the parts
  that the agent received; `discipline trimmed` is the discipline part without
  its two sections on training time. AutoDS-Tools composes the file itself;
  for Terminus-2 the same text is appended to the task statement. The texts
  are in [`result_files/instruction_file`](result_files/instruction_file).
- Image. `stock` is the image of the benchmark adaptation, `enriched` the
  image built for AutoDS-Tools with LightAutoML and the other libraries its
  file names, `FEDOT` the image with the FEDOT framework.
- Machine. All cells ran on one server (18 cores, 96 GB RAM, no GPU) with
  three exceptions: `tabred/terminus-2/enriched-image` ran on a workstation,
  and `tabred/terminus-2/stock-image` and the earlier single-attempt runs ran
  on co-authors' machines and were downloaded from Harbor Hub.
- Language models were called through OpenRouter as `google/gemma-4-31b-it`,
  `google/gemma-4-26b-a4b-it` and `z-ai/glm-4.7`.

## Layout of a job directory

Each cell directory holds one or more Harbor job directories under their
original names. A job directory holds `config.json`, `lock.json`,
`result.json` and `job.log` of the job and one directory per trial, named
`<task>__<id>`. The jobs downloaded from Harbor Hub consist of trial
directories only. A trial directory contains:

| File | Content |
|---|---|
| `config.json`, `lock.json` | configuration of the trial as Harbor resolved it: task, agent, model, environment |
| `result.json` | scorer output, token counts and cost, exception if any, start and end of each phase |
| `trial.log`, `exception.txt` | Harbor log of the trial and the traceback when the trial ended on an exception |
| `agent/trajectory.json` | the trace: every step of the agent with its tool calls and their output |
| `agent/terminus_2.pane`, `agent/recording.cast` | Terminus-2 only: the terminal contents and their recording |
| `agent/instruction.md` | AutoDS-Tools and FEDOT.LLM only: the task statement as the agent received it, including the instruction file |
| `agent/autods_trace.json`, `agent/autods.log` | AutoDS-Tools only: its own trace and log |
| `agent/fedotllm.log` | FEDOT.LLM only: its log with the fitting, search and tuning messages of the backend |
| `verifier/reward.json`, `verifier/test-stdout.txt` | the metric computed by the benchmark scorer and the scorer output |
| `artifacts/` | files exported from the container; for MLAgentBench and the case studies the submission |

The files are stored as Harbor wrote them. Absolute paths inside them refer to
the machine on which the job ran. The only edit is the address of a network
proxy, replaced by `proxy-host` in the error messages of 16 files.

An AutoDS-Tools trial that was cut at the time limit has no
`agent/trajectory.json` and no token record.

## Result files

| File | Content |
|---|---|
| [`trials.csv`](result_files/trials.csv) | one row per trial directory in `runs/`: configuration, outcome, metric, steps, duration, tokens, cost, path |
| [`cells.csv`](result_files/cells.csv) | one row per cell: configuration, jobs, number of trials, trials without a submission, trials cut at the time limit, median steps and duration, token and cost totals |
| [`tabred_published_methods.csv`](result_files/tabred_published_methods.csv) | the eighteen tuned methods published with TabReD (Rubachev et al., Table 2) |
| [`tabred_task_means.csv`](result_files/tabred_task_means.csv) | TabReD, per cell and task: number of scored trials, mean, minimum and maximum of the metric, normalised score of the mean |
| [`tabred_leaderboard.csv`](result_files/tabred_leaderboard.csv) | the published methods and the three harnesses of the main comparison: per-task values, mean normalised score, average rank (Table 3, Fig. 2) |
| [`tabred_comparisons.csv`](result_files/tabred_comparisons.csv) | paired comparisons of two configurations over the TabReD tasks (Fig. 4 and the text of Sections 5 and 6) |
| [`mlagentbench_task_means.csv`](result_files/mlagentbench_task_means.csv) | MLAgentBench, per cell and task: scored trials, trials cut at the time limit, mean, minimum and maximum (Table 4) |
| [`case_studies.csv`](result_files/case_studies.csv) | the case studies, one row per trial with every metric of the scorer (Table 5, Fig. 3) |
| [`trace_learners.csv`](result_files/trace_learners.csv) | TabReD, one row per trial of Terminus-2 and AutoDS-Tools: which learners, search procedures and settings appear in the code the agent ran (Section 7.1) |
| [`trace_discipline_clauses.csv`](result_files/trace_discipline_clauses.csv) | TabReD, per cell: number of trials whose trace shows each clause of the discipline part (Section 7.2) |
| [`trace_repair_loop.csv`](result_files/trace_repair_loop.csv) | earlier single-attempt runs, per task: reports of the AutoDS-Tools repair agent with and without the file (Section 7.3) |
| [`fedot_backend.csv`](result_files/fedot_backend.csv) | FEDOT.LLM, one row per trial: duration of the first fit, whether the structure search ran, tuning budget and metric, final pipeline (Sections 5.1 and 5.3) |
| [`instruction_file/`](result_files/instruction_file), [`instruction_file_variants.csv`](result_files/instruction_file_variants.csv) | the text of every variant of the instruction file as the agents received it, with length and SHA-256 prefix |

### Columns of `trials.csv`

| Column | Meaning |
|---|---|
| `benchmark`, `harness`, `cell` | position of the trial in `runs/` |
| `instruction_file`, `image`, `model`, `machine`, `parallel_trials` | configuration of the cell |
| `task`, `job`, `trial`, `path` | task, Harbor job, trial directory and its path in this repository |
| `counted` | `yes` if the trial enters the numbers of the paper; `no` for a trial that was repeated or not finished, with the reason in `note` |
| `outcome` | `scored`: the scorer returned the task metric. `no submission`: the scorer found no valid submission. `error`: the trial ended on an exception before scoring. `unfinished`: the job was stopped before the trial ended |
| `exception` | exception type recorded by Harbor; `AgentTimeoutError` marks a trial cut at the time limit, which is scored when a submission already exists |
| `metric`, `higher_is_better`, `value` | task metric in raw units, as written by the benchmark scorer |
| `steps` | number of steps in `agent/trajectory.json` |
| `minutes_trial`, `minutes_agent`, `minutes_to_score` | duration of the whole trial, of the agent phase, and from the start of the trial to the end of scoring |
| `input_tokens`, `cached_tokens`, `output_tokens`, `cost_usd` | usage recorded by Harbor. FEDOT.LLM calls the model from inside the container, so its tokens are read from `agent/fedotllm.log` and priced at the list price of gemma-4-31b-it, USD 0.09 and 0.34 per million input and output tokens |

### Definitions

- Normalised score. For task *j* and raw score *s*, *n_j(s) = (s - w_j) / (b_j - w_j)*,
  where *w_j* and *b_j* are the weakest and the strongest of the eighteen
  published values on that task. A cell is summarised by the mean of *n_j*
  over the tasks.
- Per-task mean. The mean over the trials of the cell that were scored.
  Trials without a submission are counted separately and do not enter the mean.
- Paired comparison (`tabred_comparisons.csv`). Difference of the normalised
  scores of the per-task means, `a` minus `b`, averaged over the tasks that
  both configurations scored; 95% bootstrap interval over tasks (20,000
  resamples); tasks won on the raw metric; exact two-sided Wilcoxon
  signed-rank test, omitted for fewer than five tasks. `fisher_p` is Fisher's
  exact test on the numbers of trials with and without a submission.
- Token and cost totals in `cells.csv` cover the trials with a usage record,
  whose number is in `trials_with_usage`.
- Trace signatures. `trace_learners.csv` searches the code and shell commands
  that the agent executed or submitted; `trace_discipline_clauses.csv`
  searches the terminal contents of Terminus-2 and the trajectory of
  AutoDS-Tools. A signature shows that the text occurs in the trace.

## Repeated trials

Thirteen trial directories have `counted = no`.

- `tabred/terminus-2/file-library`: two trials ended on an API connection
  error. They were repeated with the same command in
  `terminus-ktool2-fill-20261007-162612`.
- `tabred/terminus-2/model-gemma-4-26b-a4b-it`: one trial ended on an API
  connection error. It was repeated with the same command in
  `terminus-tabred-Msmall-fill-20261012-143233`.
- `tabred/autods-tools/model-glm-4.7`: the cell consists of three passes over
  the eight tasks. In the second and third pass four trials crashed when the
  file-search tool of the repair agent raised an exception on an absolute
  path pattern, and two trials timed out during the installation of the
  agent. The six trials were repeated in the two `...-fix-...` jobs after a
  patch to the Harbor adapter of AutoDS-Tools, which returns the error text of
  that tool to the model. The code path was not executed in any other trial.
- `case-studies/autods-tools/text-with-library-section`: two trials timed out
  during the installation of the agent and were repeated in
  `autods-cases-top-20260924-164757`.
- `mlagentbench/autods-tools/file-none_cifar10-imdb`: the job was stopped with
  two trials unfinished.

The cell `tabred/fedot-llm/library-built-in` has 28 trials. Four of them (one
of `delivery-eta`, three of `sberbank-housing`) reached the 3,600 s limit
without a submission and are counted as trials without a submission. The two
tasks were repeated until each had three scored attempts.

## Traces on Harbor Hub

The following jobs are also published on Harbor Hub, where each trial can be
browsed step by step. For regression tasks the hub shows the reward
1 / (1 + RMSE); the raw metric is in `verifier/reward.json`.

| Job on Harbor Hub | Content | Copy in this repository |
|---|---|---|
| [7593cc7b](https://hub.harborframework.com/jobs/7593cc7b-8b7e-4e5b-87c4-1c1f18527fa7) | Terminus-2 on TabReD, stock image, 24 trials | [`runs/tabred/terminus-2/stock-image`](runs/tabred/terminus-2/stock-image) |
| [77c2d2f8](https://hub.harborframework.com/jobs/77c2d2f8-722e-471a-bf44-b075776c308e) | FEDOT.LLM on TabReD: `homesite-insurance`, `homecredit-default`, `maps-routing` | [`runs/tabred/fedot-llm/library-built-in`](runs/tabred/fedot-llm/library-built-in) |
| [374be194](https://hub.harborframework.com/jobs/374be194-9097-4b57-810b-354ce774cf8d) | FEDOT.LLM on TabReD: the other five tasks | same directory |
| [b9de44ad](https://hub.harborframework.com/jobs/b9de44ad-9ef2-473e-a864-fd2e0bf7785f) | FEDOT.LLM on TabReD: repeat of `sberbank-housing` | same directory |
| [7768c071](https://hub.harborframework.com/jobs/7768c071-ce0a-4904-b323-efd106e7304d) | FEDOT.LLM on TabReD: repeat of `delivery-eta` | same directory |
| [845146bc](https://hub.harborframework.com/jobs/845146bc-7450-492a-852e-d4ae3519a78f) | AutoDS-Tools on the case studies, nine trials | [`runs/case-studies/autods-tools/text-with-library-section`](runs/case-studies/autods-tools/text-with-library-section) |
| [db04edc1](https://hub.harborframework.com/jobs/db04edc1-b853-4d34-8052-dfa186865cd8) | AutoDS-Tools on the case studies, two repeated trials | same directory |
| [3113aba7](https://hub.harborframework.com/jobs/3113aba7-1a4b-5319-9777-2c6717635bc3) | AutoDS-Tools with the file, earlier single-attempt run, 18 tasks | [`runs/earlier-single-attempt/autods-tools/file-both`](runs/earlier-single-attempt/autods-tools/file-both) |
| [56768b37](https://hub.harborframework.com/jobs/56768b37-f841-5678-8fc8-c2af1a45af7d) | AutoDS-Tools without the file, earlier single-attempt run, 18 tasks | [`runs/earlier-single-attempt/autods-tools/file-none`](runs/earlier-single-attempt/autods-tools/file-none) |
| [1a42d1fe](https://hub.harborframework.com/jobs/1a42d1fe-a3e1-4fa5-a3d4-e5338ae3ff08) | Terminus-2 on MLAgentBench, earlier single-attempt run of six tasks; the paper reports the later three-attempt cell | [`runs/mlagentbench/terminus-2/file-none`](runs/mlagentbench/terminus-2/file-none) holds the later cell |

## External resources

Benchmarks and their Harbor adaptations:

- TabReD: [repository](https://github.com/yandex-research/tabred), [paper](https://arxiv.org/abs/2406.19380)
- MLAgentBench: [repository](https://github.com/snap-stanford/MLAgentBench), [paper](https://arxiv.org/abs/2310.03302)
- Harbor tasks: [danil-e/harbor-datasets-tabred](https://huggingface.co/datasets/danil-e/harbor-datasets-tabred), [danil-e/harbor-datasets-mlab](https://huggingface.co/datasets/danil-e/harbor-datasets-mlab), tabular adapter [AaLexUser/harbor-tabred-adapter](https://github.com/AaLexUser/harbor-tabred-adapter)

Harnesses and tools:

- [FEDOT.LLM](https://github.com/aimclub/FEDOT.LLM) and its backend [FEDOT](https://github.com/aimclub/FEDOT)
- [AutoDS-Tools](https://github.com/sb-ai-lab/AutoDS-Tools); the runs install the branch [`mlab-gpu-pub` of florentiner/AutoDS-Tools](https://github.com/florentiner/AutoDS-Tools/tree/mlab-gpu-pub), as recorded in `config.json` of each trial
- Terminus-2, the reference agent of [Terminal-Bench](https://github.com/laude-institute/terminal-bench) ([paper](https://arxiv.org/abs/2601.11868))
- [Harbor](https://github.com/harbor-framework/harbor) and [Harbor Hub](https://hub.harborframework.com)
- [LightAutoML](https://github.com/sb-ai-lab/LightAutoML), the library named by the instruction file for tabular tasks
- [OpenRouter](https://openrouter.ai), through which the language models were called

Case studies:

| Case | Source | Data | Author baseline |
|---|---|---|---|
| Maize grain yield, Genomes to Fields | [Kick et al., 2023](https://doi.org/10.1093/g3journal/jkad006) | [Zenodo 6916775](https://zenodo.org/records/6916775) | Pearson *r* 0.461 |
| Exit state of jobs on Fugaku, F-DATA | [Antici et al., 2025](https://doi.org/10.1038/s41597-025-05633-1) | [Zenodo 11467483](https://zenodo.org/records/11467483) | accuracy 0.89 |
| Glass-transition temperature of polymers, OpenPoly | [Wang et al., 2025](https://doi.org/10.1007/s10118-025-3402-y) | [WangGroupFDU/Openpoly_benchmark](https://github.com/WangGroupFDU/Openpoly_benchmark) | *R*² 0.904 |

## Citation

S. Chumakov, D. Ezhov, A. Lapin, P. Marian, K. Anpilov, H. Wang, L. Goliatt,
N. O. Nikitin. Architecture over Parameters: How Far Agentic Design Patterns
Carry a Weak Model in Automated Machine Learning. Manuscript, 2026.
