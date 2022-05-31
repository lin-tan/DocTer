## Generality analysis among versions (Section 4.1) 

We list the detailed results for the evaluation of the generality across versions of the same library. We
apply the rules that DocTer constructed from TensorFlow v2.1.0, PyTorch v1.5.0, and MXNet v1.6.0 to six versions: two more recent versions from each library respectively (TensorFlow v2.2.0 and v2.3.0, PyTorch v1.6.0 and v1.7.0, and MXNet v1.7.0 and 1.8.0).

For each library, the table shows

- The number of APIs with constraints extracted (# APIs with constr. extracted)
- The total number of constraints extracted (row # constr. extracted)
- The number of constraints extracted per API (row # constr. per API: Avg (Min-Max))
- The number of parameters in the evaluation set (row # evaluated param.)
- The number of the parameters in the evaluation set with at least one constraint (row # evaluated param. with constr.)
- The number of constraints manually labeled in the evaluation set (row # evaluated constr.)
- The precision, recall, and F1 score of all constraints (row Precision/Recall/F1 for All (%))
- The precision, recall, and F1 score of each category (row Precision/Recall/F1 for \<category\> (%))
  
  
The Total/Avg column shows the total number of parameters in the evaluation set and constraints as well as the average precision, recall, and F1 score.



|                                         | TensorFlow (v2.2.0&v2.3.0) | PyTorch (v1.6.0&v1.7.0) | MXNet (v1.7.0&v1.8.0) | Total/Avg      |
|-----------------------------------------|----------------------------|-------------------------|-----------------------|----------------|
| # APIs with constr. extracted           | 4,547                      | 1,086                   | 2,051                 | 7,684          |
| # constr. extracted                     | 38,791                     | 6,850                   | 14,295                | 59,936         |
| # constr. per API: Avg (Min-Max)        | 8.5 (1-44)                 | 6.3 (1-28)              | 7.0 (1-111)           | 7.3 (1-61)     |
| # evaluated param.                      | 190                        | 93                      | 320                   | 603            |
| # evaluated param. with constr.         | 173                        | 81                      | 227                   | 481            |
| # evaluated constr.                     | 378                        | 151                     | 442                   | 971            |
| Precision/Recall/F1 for All (%)         | 87.3/73.5/79.8             | 74.7/82.6/78.4          | 83.7/76.9/80.2        | 81.9/77.7/79.5 |
| Precision/Recall/F1 for dtype (%)       | 92.1/84.8/88.3             | 75.0/80.0/77.4          | 89.4/82.5/85.8        | 85.5/82.4/83.8 |
| Precision/Recall/F1 for structure (%)   | 78.3/90.0/83.7             | 100.0/95.2/97.6         | 82.6/88.2/85.3        | 87.0/91.1/88.9 |
| Precision/Recall/F1 for shape (%)       | 82.1/65.7/73.0             | 72.3/100.0/84.0         | 64.3/55.1/59.3        | 72.9/73.6/72.1 |
| Precision/Recall/F1 for valid value (%) | 80.0/18.2/29.6             | 46.7/41.2/43.7          | 96.3/78.8/86.7        | 74.3/46.1/53.3 |
