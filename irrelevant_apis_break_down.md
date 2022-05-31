## Irrelevant APIs (Section 3)

There are in total 5,224 APIs (2,334 from TensorFlow 2.1.0, 874 from PyTorch v1.5.0, and 2,016 from MXNet v1.6.0). We filter out 2,666 APIs in total due to the five reasons we list in Section 3. The breakdown is listed in the following table.



|                   |                                           | TensorFlow v2.1.0 | PyTorch v1.5.0 | MXNet v1.6.0 | Total |
|-------------------|-------------------------------------------|-------------------|----------------|--------------|-------|
| Total #APIs       |                                           |              2334 |            874 |         2016 | 5224|
| # Relevant APIs   |                                           |              1008 |            529 |         1021 | 2558|
| # Irrelevant APIs | Total                                     |              1326 |            345 |          995 | 2666|
|                   | (1)deprecated                             |               571 |              9 |          847 | 1427|
|                   | (2)has no input argument                  |                47 |             62 |           28 |137|
|                   | (3)cannot be parsed                       |                13 |             16 |           15 |44|
|                   | (4)is a non-layer class constructor       |               490 |            180 |           68 |738|
|                   | (5)has no “parameter” description section |               205 |             78 |           37 |320|