# **1. Repository Information**

This repository contains the data produced during the work discussed in in the paper "[Towards quantum gravity with neural networks: Solving quantum Hamilton constraints of 3d Euclidean gravity in the weak coupling limit](https://arxiv.org/abs/2405.00661)". Please refer to this paper for more details on how the data was produced.



# **2. Citing**

Please cite the paper mentioned above if you use the data. The citation is:

H. Sahlmann and W. Sherif, "* *Towards quantum gravity with neural networks: Solving quantum Hamilton constraints of 3d Euclidean gravity in the weak coupling limit,* *" [arXiv:2405.00661 [gr-qc]] (2024).



# **3. File Description**

In this repository, you will find 4 general directories (here called parent directories):

1. Ground Energy + Fluctuations
2. Misc
3. Quantum Constraint
4. Volume

Each of these directories correposnd to different data produced and discussed in the corresponding parts in the paper mentioned above (e.g. the directory "Ground Energy + Fluctuations" contains the data used in Table 1 and Table 2 in the paper while the "Volume" directory contains the data used in Section 4.3 of the paper). Some of these parent directories, which involve simulations solving constraints, contain within them several sub-directories (child directories) corresponding to different produced data. The raw data of the simulation can be found in a `.json` file inside the child directories.



# **4. Usage**

## **4.1 Raw Simulation Data**

The `.json` files include the raw data produced during the study. These files can be easily accessed using a python script, as an example, by using:

```
import json

filePath = ...

data = json.load(open(filePath))
```

where `filePath` should hold the correct path to the local data once downloaded. Once loaded, the data is handled as a python `dict`.



The dictionary will have * *at least one* * parent key called "Energy". The data in the "Energy" key corresponds to the data being minimised. The data in any other parent key correspond to operators which were being observed during the simulation. For example, in the data in the "Quantum Constraint" directory, some `.json` files will have multiple parent keys such as FG, H, HG, .... Each of these keys correspond to different operators which were observed during that simulation. Each parent key is yet another dictionary in itself. The structure of the dictionaries corresponding to any parent key are always the same and always include the keys:

1. iters
2. Mean
3. Variance
4. Sigma
5. R_hat
6. TauCorr

Hence, to access the "Mean" values, you use `data["Energy"]["Mean"]` (or alternatively `data["FG"]["Mean"]` if you wish to observe the value of the F + G operator during the simulation). The data represents the values during a simulation of typically 500 iterations, hence, each of the keys mentioned above will correspond to an array of 500 items. The iters array includes merely the iteration number. The Mean array includes the value of the expectation value of the constraint at the corresponding iteration. The Variance, Sigma, R_hat and TauCorr includes the values of the variance and error in the expectation value at the given iteration as well as the split R-hat diagnostic and the time correlation also in the given iteration. 



## **4.2 Variational State Data**

Additionally, some child directories should include a `.npy` file, which holds the amplitudes of the variational state for the given simulation. However, these files are rather large, and exceed the allowed maximum file size here. Therefore, they will be hoted on a Github page here. The page will have also all the files available in this repository but in addition to the variational state files as well. These files should be loaded using numpy in python. For example:

```
import numpy as np

filePath = ...

varState = np.load(filePath)
```

This will load the amplitudes as an array into the `varState` variable.



## **4.3 Fluctuation results**

In some child directories, there will be a `.txt` file which includes the output of the calculation of the expectation value of some operators and their quantum fluctuations. These are only results, and not data, as the data can only be computed during the simulation.



## **4.4 Probabilities**

The "Misc/Probabilities" directory contains `.npy` files which should be handled in the same manner as the variational states. These files correspond to the probability simulations conducted in section 4.4.4 in the paper.



## **5. References**

The data provided in this repository was produced using the [NetKet](https://github.com/netket) (1) package

(1) [doi: 10.21468/SciPostPhysCodeb.7](https://doi.org/10.21468/SciPostPhysCodeb.7)
