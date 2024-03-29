# DocTer



## Paper
DocTer: Documentation-Guided Fuzzing for Testing Deep Learning API Functions (ISSTA'22) 


## Tool
We release our tool DocTer on the Docker Hub. Please see the instruction to run DocTer in ([`./DocTer_instructions.md`](https://github.com/lin-tan/DocTer/blob/main/DocTer_instructions.md))



## Details

We share the following data:


- [The bug list](https://docs.google.com/spreadsheets/d/1DgupQBMVpybHtyOhCO0fRb-oJDZbZSbo7H-AG36AE_c/edit?usp=sharing).

- Annotation details ([`./annotation_details`](https://github.com/lin-tan/DocTer/tree/main/annotation_details)): including the annotated data of 30% of the parameters, the keywords we used for normalization (Section 2.2) and the full list of assumptions we made during annotation (Section 2.2)

- Constraints extracted ([`./constraints_extracted`](https://github.com/lin-tan/DocTer/tree/main/constraints_extracted)): The extracted constraints for 2,415 APIs.


- The details of generality analysis among versions (Section 4.1) ([`./generality_among_versions.md`](https://github.com/lin-tan/DocTer/blob/main/generality_among_versions.md)).

- The extended results of the impact of fuzzer’s nondeterminism (Section 4.3) ([`./fuzzer_nondeterminism.md`](https://github.com/lin-tan/DocTer/blob/main/fuzzer_nondeterminism.md)).

- The break down of all analyzed APIs (Section 3) ([`./irrelevant_apis_break_down.md`](https://github.com/lin-tan/DocTer/blob/main/irrelevant_apis_break_down.md)).



For further details, please check the `README.md` in each individual folder.





