# New Relic

## NRQL
- By default NRQL queries do not return all results. You have to specify
 a time frame/window for which you expect the results to show up.
 So `SELECT * FROM blah` will not return all results.
 You have to do for example: `SELECT * FROM blah SINCE 1 day ago`.
