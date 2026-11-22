# Continuous Intelligence System Assessment

Continuous Intelligence | Project 06 | Example Report

## Overview

This project integrates signal design,
anomaly detection, and system assessment
into a continuous intelligence pipeline.

The objective is to transform operational measurements
into interpretable indicators of system behavior
and produce an overall assessment of system state.

## Data

The example dataset contains 60 observations
of system activity.

Each observation records:

- Requests handled.
- Errors encountered.
- Total response time in milliseconds.

The dataset includes a period of elevated
errors and response times.

[View Example Dataset](https://github.com/denisecase/cintel-06-continuous-intelligence/blob/main/data/system_metrics.csv)

## Methods

The pipeline applies three analytical steps.

### 1. Signal Design

Raw measurements are transformed into:

- Error rate: errors divided by requests.
- Average latency: total latency divided by requests.

### 2. Anomaly Detection

Individual observations are flagged when:

- Error rate exceeds 5%, or
- Average latency exceeds 40 milliseconds.

### 3. System Assessment

The pipeline calculates mean values
across all observations.

It classifies the overall system state as:

- `STABLE` when neither mean signal exceeds its threshold.
- `DEGRADED` when either mean signal exceeds its threshold.

## Results

The example produces the following assessment.

| Metric               |   Result |
| -------------------- | -------: |
| Average requests     |   157.35 |
| Average errors       |     4.43 |
| Average error rate   |    2.65% |
| Average latency      | 33.71 ms |
| Overall system state |   STABLE |

The pipeline also identifies **7 anomalous observations**
using its individual-observation thresholds.

[View System Assessment](https://github.com/denisecase/cintel-06-continuous-intelligence/blob/main/artifacts/system_assessment.csv)

## Interpretation

The overall assessment is `STABLE`
because the average error rate and latency
remain below their configured thresholds.

However, several individual observations
exceed the anomaly thresholds.

This distinction is important.

A system may appear stable when summarized
across an entire observation period
while experiencing shorter episodes
of degraded performance.

Monitoring should consider both overall
conditions and localized anomalies.

## Limitations

The example assessment is based on aggregate
means and fixed thresholds.

It does not yet incorporate rolling-window analysis,
reference-period drift comparisons,
or persistent alerting.

The final assessment artifact contains summary metrics
but does not preserve the individual anomaly records.

A more complete system could retain
observation-level evidence and combine
rolling monitoring, drift detection,
and system-state classification.

## Conclusion

Continuous intelligence connects measurements,
signals, analytical rules, and interpretation.

The example demonstrates how several techniques
can contribute to an assessment of system behavior.

Its most important finding is that
**an overall stable classification does not guarantee
that every observation was within acceptable limits.**

Effective monitoring requires both summary assessments
and sufficient detail to investigate anomalous conditions.

## Documentation Index

- **Home** - this landing page
- [**Project Instructions**](project-instructions.md)
- [**Glossary**](glossary.md)
- [**API**](api.md)
- [**Reactive App**](./app/index.html)

## Project Links

- [GitHub Repository](https://github.com/denisecase/cintel-06-continuous-intelligence)
- [Example Pipeline](https://github.com/denisecase/cintel-06-continuous-intelligence/blob/main/src/cintel/continuous_intelligence.py)
- [Results and Artifacts](https://github.com/denisecase/cintel-06-continuous-intelligence/tree/main/artifacts)

## Project Resources

- [Project Instructions](project-instructions.md)
- [Professional Python Guide](https://denisecase.github.io/pro-analytics-02/)
- [Professional Python Project Explainer](https://pup-pack.github.io/professional-python-project-explainer/).
- [Suggested Datasets](https://denisecase.github.io/pro-analytics-02/reference/datasets/cintel/)

## Custom Application: Project Request Performance Monitoring

### Question

Can project request data identify when workload and response time indicate
project-performance problems?

### Data

I created a synthetic dataset in
`data/project_metrics.csv`. The data represents project requests,
overdue requests, and total response time.

In this application, `requests` represents project requests,
`errors` represents overdue requests, and `total_latency_ms` represents
total response time.

### Process and Tools

The Python pipeline uses Polars to calculate average requests, average
overdue requests, overdue-request rate, and average response time.
It compares the results with monitoring thresholds and classifies the
project performance as STABLE or DEGRADED.

The project uses Python, Polars, uv, GitHub, and Zensical.

### Results

| Metric | Average | Threshold | Result |
|---|---:|---:|---|
| Project requests | 111.5 | Informational | Workload increased across the observations |
| Overdue-request rate | 2.43% | 2.00% | Exceeded the threshold |
| Average response time | 24.34 ms | 40.00 ms | Within the threshold |
| Overall project state | DEGRADED | — | Overdue-request rate requires attention |

### Interpretation

The project was classified as DEGRADED because the average overdue-request
rate of 2.43% exceeded the 2% threshold. Average response time remained
below the 40-millisecond threshold, so response speed was not the main
cause of the classification.

This shows how continuous intelligence can identify a project-performance
issue even when response time remains acceptable.

### Limitation and Next Steps

The data is synthetic and does not include task priority, project
complexity, seasonal workload, or timestamps. If I continued this project,
I would collect real project data, add priority and due-date fields, and
monitor performance over time.
