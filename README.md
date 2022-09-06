# MODIG
## MODIG: Integrating Multi-Omics and Multi-Dimensional Gene Network for Cancer Driver Gene Identification based on Graph Attention Network Model
MODIG is a GAT-based model designed for generating gene repre-sentation from a multi-dimensional gene network for the identifica-tion of cancer driver genes, which mainly performed three steps to integrate multi-omics data and multiple gene associations. 

Firstly, it generates multiple gene association profiles based on PPI, gene sequence similarity, gene tissue-specific expression profiles, gene pathway membership, and GO annotation information. 

Secondly, a multi-dimensional gene network is constructed using these gene association profiles as multiple edges and multi-omics features as node attributes. 

Thirdly, to learn knowledge from the multi-dimensional graph, instead of fusing different edges into a single edge to form a homogeneous graph, MODIG applies a GAT block for within-dimension interactions to get the dimension-specific gene representations and a joint learning module to adapta-tively learn the importance of different dimensional representa-tions and fuse them by an attention mechanism for downstream cancer driver gene prediction.


# Overview
Here we provide an implementation of MODIG in Pytorch and PyTorch Geometric. The repository is organised as follows: 
- `modig_graph.py`    generate multi-dimensional gene networks as input.
- `modig.py`  the implementation of MODIG.
- `main.py`   the main script of MODIG.
- `utils.py`  functions used in MODIG.
- `omic_preprocess.py` omics_data processing script of MODIG.

You can download the necessary dataset file from [here](https://doi.org/10.5281/zenodo.7053224), which contains labels for training, omics feature matrix, ppi network, gene association profiles. Please Download the datasets, unzip and put the data folder in the same path as thee modig folder.

## Requirements
- Python 3.8
- Pytorch 1.8.1+cu102
- Pytorch Geometric 2.0.0
- networkx 2.6.3
- numpy 1.21.2
- scipy 1.7.1
- sklearn 0.24.2
- pandas 1.3.3


# Implementation
## Step 1: Download and decompress data files
You can unzip the datasets by `unzip data.zip`. 

- `Data/feature`    contains processed omics feature matrix generated by `omic_preprocess.py`.

- `Data/label`  contains labeled genes (positive/negative genes) for training.

- `Data/ppi`    contains edges of ten different ppi networks used in the paper.

- `Data/simmatrix`  contains four processed gene association files that can be used in `modig_graph.py` to generate multi-dimensional gene networks.

## Step 2: Run the model
You can run `python main.py -t output -ppi CPDB`

Note there are several parameters can be tuned: --thr_go, --thr_seq, --thr_exp, --thr_path, etc. Please refer to the main.py file for detailed description of all parameters.
