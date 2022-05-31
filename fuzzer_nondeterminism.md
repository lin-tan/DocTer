## Impact of Fuzzer’s Nondeterminism (Section 4.3)

Specifically, we repeat the fuzzing experiment (with the same set of extracted constraints) eight times. For each run, we generate 2,000 test inputs for the baseline and 2,000 test inputs for DocTer for all APIs from the three libraries. In each run, we use the same random seed for both the baseline and DocTer. Different runs use different seeds. Since it requires significant manual effort to inspect the detected bugs from all eight runs, which are 2,301 API crashes to examine, we use the number of buggy APIs (i.e., the number of APIs that crash) to indicate the fuzzers’ effectiveness. Overall, among the eight runs, DocTer on average detects 172.0 buggy APIs while the baseline on average detects 115.6 buggy APIs. We perform the Mann-Whitney U-test and confirm the improvement is statistically significant with a p-value of 0.0004 and the Cohen’s d effect size of 8.96 (effect size more than 2.0 is huge). 


Here, we list all results for the 8 runs for Baseline  (Table A) and DocTer (Table B), as well as the break down of CI (Table C) and VI (Table D) mode.


### Table A

|            | Baseline1 | Baseline2 | Baseline3 | Baseline4 | Baseline5 | Baseline6 | Baseline7 | Baseline8 | Average |
|------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|---------|
| TensorFlow | 83        | 87        | 90        | 79        | 81        | 81        | 83        | 81        | 83.1    |
| PyTorch    | 6         | 8         | 8         | 8         | 6         | 7         | 6         | 11        | 7.5     |
| MXNet      | 29        | 28        | 27        | 21        | 27        | 21        | 27        | 20        | 25.0    |
| Total      | 118       | 123       | 125       | 108       | 114       | 109       | 116       | 112       | 115.6   |



### Table B 

|            | DocTer1 | DocTer2 | DocTer3 | DocTer4 | DocTer5 | DocTer6 | DocTer7 | DocTer8 | Average |
|------------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
| TensorFlow | 102     | 108     | 110     | 114     | 111     | 103     | 103     | 111     | 107.8   |
| PyTorch    | 27      | 27      | 29      | 28      | 27      | 29      | 29      | 29      | 28.1    |
| MXNet      | 37      | 32      | 45      | 32      | 36      | 35      | 35      | 37      | 36.1    |
| Total      | 166     | 167     | 184     | 174     | 174     | 167     | 167     | 177     | 172.0   |

### Table C

|            | CI1 | CI2 | CI3 | CI4 | CI5 | CI6 | CI7 | CI8 | Average |
|------------|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| TensorFlow | 83  | 88  | 89  | 93  | 86  | 85  | 86  | 92  | 87.8    |
| PyTorch    | 23  | 25  | 25  | 23  | 24  | 25  | 24  | 22  | 23.9    |
| MXNet      | 25  | 24  | 36  | 27  | 28  | 26  | 31  | 30  | 28.4    |
| Total      | 131 | 137 | 150 | 143 | 138 | 136 | 141 | 144 | 140.0   |


### Table D


|            | VI1 | VI2 | VI3 | VI4 | VI5 | VI6 | VI7 | VI8 | Average |
|------------|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| TensorFlow | 78  | 84  | 84  | 83  | 91  | 81  | 78  | 88  | 83.4    |
| PyTorch    | 23  | 20  | 23  | 25  | 22  | 22  | 24  | 26  | 23.1    |
| MXNet      | 29  | 25  | 26  | 27  | 25  | 27  | 24  | 27  | 26.3    |
| Total      | 130 | 129 | 133 | 135 | 138 | 130 | 126 | 141 | 132.8   |