# CAEclust : A consensus of autoencoders representations for clustering

<span style="color:red"><b>This project is currently under submission process. The source will be made available soon!</b></span>

This repository contains the source code for **CAEclust** **V1.0** (**C**onsensus of **A**uto**E**ncoders representations for **clust**ering), python package that implements an original deep spectral clustering in an ensemble framework. 

Recently, strategies combining classical clustering approaches and deep autoencoders have been proposed, but their robustness is impeded by deep network hyperparameters settings. We alleviate this issue with a consensus solution that hinges on the fusion of multiple deep autoencoder representations and spectral clustering. 

![](./images/images_readme/Scheme_clustering_final.png)

**CAEclust** offers an efficient merging of *encodings* by using the *landmarks* strategy and demonstrates its performance and robustness on benchmark data. **CAEclust** enables to reproduce our experiments and explore novel datasets. 



## Software Architecture and Functionalities

We summarize the package usage in the following figure and detail below **CAEclust**  functionalities.

<img src="./images/images_readme/package_overview_vertical_crop_small.png" alt="scale=" style="zoom:&80%;" />



**[io]** *[dataLoader.py](./CAEclust/io/dataLoader.py)* loads a dataset. **CAEclust** proposes by default two well-known benchmark images datasets, namely *USPS* and *MNIST*.

**[daeNet]** *[daeEncoding.py](./CAEclust/daeNet/daeEncoding.py)* sets a DAE with general parameters (e.g. optimizer function, number of epochs, batch size, encoding dimension), and any layer number and width. The method *deep\_ae()* generates the encoded data. The package proposes to generate the encodings either in serial (*serial\_encodings.py*) or in parallel (*parallel\_encodings.py*). 

**[clustering]** *[ensClust.py](./CAEclust/clustering/ensClust.py)* computes the ensemble sparse affinity matrix with the method *ensemble\_approximate\_affinity()*. The deep consensus clustering is then obtained from the shared space **B** using the *sparse\_SVD()*.

**[evaluation]** *[evaluation.py](./CAEclust/eval/evaluation.py)* provides 2D and 3D visualizations of the shared space **B** with *commonSpace\_plot()*. These visualizations are also proposed with the *UMAP* transformation. When studying benchmark datasets with ground truth labels, *allMetrics()* function can compute three informative metrics (accuracy, NMI, and ARI). Furthermore, *compare\_metrics()* provides an *html* summary table to easily compare the **CAEclust**  results with other clustering algorithms.



## Installing

Download and unzip the *CAEclust_package.zip* file. We recommand an installation of CAEclust within a mini [conda environment (4.11.0)](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html).

**Install miniconda for python 3.8**

Miniconda installers can be dowloaded from [here](https://docs.conda.io/en/latest/miniconda.html). Installation guidelines for various OS are listed below:

- **[Linux](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html)**

- **[Windows](https://docs.conda.io/projects/conda/en/latest/user-guide/install/windows.html)**

- **[macOS](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html)**

**Create a conda environment for python 3.8**

```shell
conda create -n CAEclustEnv python=3.8
conda activate CAEclustEnv
```

*NB: In case the **conda** command is **not found**, close your current terminal window and open a new terminal window.*

**Install python packages in the conda environment**

```shell
conda install scikit-learn matplotlib pandas jupyter ipykernel
conda install -c anaconda jinja2
conda install -c conda-forge umap-learn
pip install numpy==1.20.0
```

```shell
conda install -c conda-forge tensorflow=2.7 -v
```

*NB: tensorflow installation may take several minutes if you used a miniconda install*.

**Add your conda environment to jupyter kernel**

```shell
python -m ipykernel install --user --name=CAEclustEnv
```

**Launch** *jupyter notebook* and access the **notebooks** *(Caution: CAEclustEnv kernel should be set)*

```shell
cd CAEclust_package
jupyter notebook
```

## Quick start

**CAEclust**  package includes two types of tutorial notebooks. 

**(1)** [**Baseline\_evaluations**](./notebooks) These first notebooks show the influence of the *Deep AutoEncoder* (DAE) structure on the clustering for a non ensemble approach. 

Example of runs:<br>
- [Baseline\_evaluations for MNIST](./images/Baseline_evaluations/Baseline_evaluations_MNIST.html)<br>
- [Baseline\_evaluations for USPS](./images/Baseline_evaluations/Baseline_evaluations_USPS.html)

**(2)** [**Ensemble\_evaluations**](./notebooks) This second notebook demonstrates the performance and robustness of the **CAEclust**  consensus deep clustering.

Example of runs:<br>
- [Ensemble\_evaluations for MNIST](./images/Ensemble_evaluations/Ensemble_evaluations_MNIST.html)<br>
- [Ensemble\_evaluations for USPS](./images/Ensemble_evaluations/Ensemble_evaluations_USPS.html)

## Authors
- Severine Affeldt *([severine.affeldt@u-paris.fr]())*
- Lazhar Labiod *([lazhar.labiod@u-paris.fr]())*
- Mohamed Nadif *([mohamed.nadif@u-paris.fr]())*

## License
GPL-3.0

## References
Affeldt S, Labiod L, and Nadif M.; *CAEclust : A consensus of autoencoders representations for clustering*
