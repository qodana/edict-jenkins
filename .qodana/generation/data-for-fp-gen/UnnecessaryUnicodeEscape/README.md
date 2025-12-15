# Benchmark Data for FP Generation: UnnecessaryUnicodeEscape

This directory contains data prepared for the first generation round (FP generation).

## Files

### extractedRuleMeta.json
Contains the rule metadata with verification examples as MetaProblems.
- `ruleId`, `ruleName`, `description`, `language`, `severity` - rule metadata
- `examples` - code snippets showing violations
- `verification.before` - MetaProblem used for positive verification
- `verification.after` - null (populated in stage 1 with FP example)
- `commitReference` - git revision for file content retrieval

### truePositivesAll.json
All true positive problems from the baseline SARIF report (full SARIF Result objects).
Used as source of truth for MetaProblem -> SARIF Result restoration.

### truePositivesMeta.json
All true positives as MetaProblems (lightweight representation).
Contains: message, contextSnippet, equalIndicatorV2.

### chosenAdditionalExamples.json
MetaProblems corresponding to file revisions used as additional positive examples.
These are beyond the primary verification example in extractedRuleMeta.json.

## How This Data Is Used

1. **Loading**: `extractedRuleMeta.json` is loaded and MetaProblems are restored to SARIF Results
   using `truePositivesAll.json` (matching by equalIndicatorV2).
2. **FileRevision**: SARIF Results are converted to FileRevisions for inspection generation.
3. **Generation**: Inspections are generated using positive examples only.
4. **Analysis**: Generated inspections are run against the codebase.
5. **Classification**: Results are classified into TP/FP for the next stage.