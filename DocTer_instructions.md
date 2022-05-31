# DocTer

We release the code on Docker Hub. Step 0 is an instruction of pulling the docker image and setup the environment. The following steps are instructions of rule cosntruction, constraints extraction, and fuzzing. 


## Step 0: Pull the DocTer images

First, pull the docker image to local:
```
docker pull dnxie/docter:latest
```
You can also find it at https://hub.docker.com/repository/docker/dnxie/docter



Use the following command to start a docker container:
```
docker run -it dnxie/docter:latest
```


The default path should be `/home/code/DocTer/`, but please make sure you are at the correct path by running:
```
cd /home/code/DocTer/
```

**If you want to run the fuzzer directly and skip the constraint extraction part, please directly go to Step 2.**


## Step 1: Extract constraints


### Step 1.1: Start the Stanford Core NLP Server

To analyze the document and extract constraints, start the stanford core nlp server at the backend which will be listening the port 9000.

#### (a) Start a screen session:

```
screen
```

#### (b) Go to the directory

```
cd stanford-corenlp-full-2018-02-27
```

#### (c) Start the server
```
java -mx4g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer \
    -preload tokenize,ssplit,pos,lemma,ner,parse,depparse \
    -status_port 9000 -port 9000 -timeout 15000 &
```

After it deploys successfully, you will see the following information:

```
[main] INFO CoreNLP - StanfordCoreNLPServer listening at /0.0.0.0:9000
```

#### (d) Detach from the screen
Detach the screen with: `CTRL`+A+D


### Step 1.2: Construct rules and extract constraints

To construct the rules and extract constraints, follow the following steps: 

#### (a) Go to the directory

```
cd constraint_extraction
```

#### (b) Run the script

Run the corresponding command to start the rule construction and constraint extraction process:
- For Tensorflow: `bash run.sh tensorflow toy`
- For Pytorch: `bash run.sh pytorch toy`
- For MXNet: `bash run.sh mxnet toy`



We prepare 10 APIs for each library as toy examples. For each of the three libraries. To extract constraints for ALL APIs, simply replace `toy` with `all` in the above commands. 

**Time:**
it takes 1-3 minutes to finish this step with the toy examples, and 10-25 minutes for all APIs. 




### Step 1.3: Inspect the extracted contraints
(Current path: `/home/code/DocTer/constraint_extraction`)


The constructed rules can be found at:



- Tensorflow: `./data/tf/rules.yaml `
- PyTorch: `./data/pt/rules.yaml `
- MXNet: `./data/mx/rules.yaml `

The extracted constraints can be found at:
- Tensorflow: `./constraints/tensorflow/`
- PyTorch: `./constraints/pytorch/`
- MXNet: `./constraints/mxnet/`




## Step 2: Fuzzing



### Step 2.1: Run the fuzzer



#### (a) Go to the directory
```
cd /home/code/DocTer
```

#### (b) Run the fuzzer

**Quick start: Tensorflow CI mode with example APIs**

For example, to run the fuzzer for Tensorflow CI mode with example APIs, use the following command:

```
bash run_fuzzer.sh tensorflow ./example_constr/tf2.1 ./configs/ci.config | tee /home/workdir/tf_ci.log
```



The script `run_fuzzer.sh` calls the fuzzer and takes three parameters:
- 1. Target library name. One of `tensorflow`, `pytorch`, or `mxnet`.
- 2. Constraint folder path. Again, we prepare 10 APIs for each libaray as toy examples. The example constraints (APIs) and all constraints (APIs) can be found at: :
  - Tensorflow (example APIs): `./example_constr/tf2.1/`
  - PyTorch (example APIs): `./example_constr/pt1.5/`
  - MXNet (example APIs): `./example_constr/mx1.6/`
  - Tensorflow (all APIs): `./all_constr/tf2.1/`
  - PyTorch (all APIs): `./all_constr/pt1.5/`
  - MXNet (all APIs): `./all_constr/mx1.6/`
  
- 3. The configuration file. We prepare config files for the baseline, CI, and VI mode located at:
   - Baseline: `./configs/baseline.config`
   - CI mode: `./configs/ci.config`
   - VI mode: `./configs/vi.config`


**Time:**
For each library, it takes the fuzzer 9-27 min to finish for only the example APIs, and 40-90 hours for all APIs.




### Step 2.2: Get bug list

After the fuzzing procedure, to get a list of unexpected behaviors, use the following command if it is **Tensorflow CI mode**:

```
bash scripts/prepare_bug_list.sh /home/workdir/tensorflow/conform_constr/
``` 


The folder `/home/workdir/tensorflow/conform_constr/` was created by the fuzzer in Step 2.1. For other library or mode, replace the folder path with the corresponding path.  


Then, you will find a file called `bug_list` generated in: 
```
/home/workdir/tensorflow/conform_constr/bug_list
```
The file is in csv format and lists all the unexpected behaviors.


Specifically, we only consider/collect: 
- 1. Segmentation fault
- 2. Floating point exceptions
- 3. Abort
- 4. Bus errors


### Step 2.3: Reproduce a bug

In the file `bug_list`, the **last column**, i.e., the `Input` column, is the path to the script which takes record of the buggy inputs. To reproduce a bug, simply run the script:

```
bash <path to the script>
```



For example, 

**(This is just an example. This particular bug is not guaranteed to be detected at each run. And the path and folder name may vary depending on the target library (e.g., tensorflow) and the mode. To reproduce a particular bug, copy the last column from the file `bug_list`)**

if the path is `/home/workdir/tensorflow/conform_constr/tf.keras.layers.AveragePooling3D.yaml_workdir/Floating_Point_Exception_script_record`, which indicates that the fuzzer detects a Floating Point Exception with the API `tf.keras.layers.AveragePooling3D` in Tensorflow CI mode. 

To reproduce the bug, run:
```
bash /home/workdir/tensorflow/conform_constr/tf.keras.layers.AveragePooling3D.yaml_workdir/Floating_Point_Exception_script_record
```

Then, you can see the inputs causing the corresponding buggy behavior, in this case, Floating Point Exception. 












