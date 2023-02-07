# DAMF
### Introduction
For the sake of reproducibility, here is the code for the experiment for the paper "Accelerating Dynamic Network Embedding with Billions of Parameter Updates to Milliseconds" submitted to **KDD2023**  . In order to provide maximum reproducibility, in this code repository we provide:

- **DAMF**: A runnable code for DAMF. This includes, among other things, the full DAMF (which requires a more complex setup process) and a DAMF without the PPR enhancements (which is much simpler to setup).

- **Datasets**: Some of the datasets used for the experiments in our paper. As the datasets used in our experiments are large, due to the space limit, we have only included a small part of datasets.

- **Evaluator**: Code for generating training and test data, as well as code for measuring node classification, link prediction and graph reconstruction tasks.

- **Baseline replicated by us**: As we did not find the code for LocalAction, we replicated it ourselves in python, which will also be made public here.


### Setup
The dynamic embedding enhancements using PPR are partially code using C++ and boost. 
If you don't need dynamic embedding enhancements, you just need the following python dependency packages installation command (simple version), otherwise you need to install boost and compile the dynamic embedding enhancement module.

We are using python version 3.9.12 and install the dependency packages with the following command:

```
pip install -r requirements.txt
```

(Optional) To install the dynamic embedding enhancement module, you may need to make sure that C++, cmake and BLAS (e.g. OpenBLAS) are already installed and run the following command:

```
mkdir build
cd build
cmake ..
make
cd ..
```

### Demo

If everything is ready, try the following demo, which adds the points of the wiki dataset in turn to a graph initialized with 1000 nodes and computes and updates the 128-dimensional embedding. the generated results will be exported to embds/wiki.
```
python DAMF1.py
cd eval
python nc.py
```


### Embedding


```
python DAMF1.py --data [data name] --type ["train", full]
```

```
python DAMF.py --data [data name] --type ["train", full]
```

### Evaluate

Node Classification
```
python nc.py --data [data name] --algo [damf, damf1]
```
Link prediction
```
python lp.py --data [data name] --algo [damf, damf1]
```
Graph reconstruction
```
python gr.py --data [data name] --algo [damf, damf1]
```


### Baseline(LocalAction)
```
python LocalAction.py --data [data name] --type ["train", "full"]
```