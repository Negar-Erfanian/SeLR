# "Code will be released (TBA)"



## Computation offloading in edge networks

## Abstract 
This paper introduces a novel computational approach for offloading sensor data processing tasks to servers in edge networks for better accuracy and makespan. 
A task is assigned with one of several offloading options, each comprises a server, a route for uploading data to the server, and a service profile that specifies the  performance and resource consumption at the server and in the network.
This offline offloading and routing problem is formulated as mixed integer programming (MIP), which is non-convex and HP-hard due to the discrete decision variables associated to the offloading options.
The novelty of our approach is to transform this non-convex problem into iterative convex optimization by relaxing integer decision variables into continuous space,  
combining primal-dual optimization for penalizing constraint violations and reweighted $L_1$-minimization for promoting solution sparsity, which achieves better convergence through a smoother path in a continuous search space. 
Compared to existing greedy heuristics, our approach can achieve a better Pareto frontier in accuracy and latency, scales better to larger problem instances, and can achieve a 7.72--9.17$\times$ reduction in  computational overhead of scheduling compared to the optimal solver in hierarchically organized edge networks with 300 nodes and 50--100 tasks.

```latex
@misc{erfaniantaghvayi2025selrsparsityenhancedlagrangianrelaxation,
      title={SeLR: Sparsity-enhanced Lagrangian Relaxation for Computation Offloading at the Edge}, 
      author={Negar Erfaniantaghvayi and Zhongyuan Zhao and Kevin Chan and Ananthram Swami and Santiago Segarra},
      year={2025},
      eprint={2505.00848},
      archivePrefix={arXiv},
      primaryClass={cs.NI},
      url={https://arxiv.org/abs/2505.00848}, 
}
```

Preprint <https://arxiv.org/abs/2505.00848v1>

## Code:

This package provides task allocation schemes in edge networks


## Clone from GitHub

Before pulling docker image, first clone the project into desired directory:

```
git clone git@github.com:Negar-Erfanian/SeLR.git ~/SeLR
```

## Configure docker container on the server
In ssh command, pull the following pytorch docker image

```
docker pull pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime
```

Then launch the container


```
docker run --runtime=nvidia --rm -it \
  -v ~/SeLR-debug:/pytorch/SeLR-debug \
  -w /pytorch/SeLR-debug \
  -p 8400:8888 \
  pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime \
  bash -c "pip install jupyter && jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root"

```

Access the jupyter interface of the container from browser, and launch a terminal from jupyter


`cd SeLR`

`pip3 install -r requirements.txt`

Test if everything is ok from the jupyter terminal

```
bash bash/generate_data_standard.sh
```

This outputs network configurations for the rest of the experiments.

if you have "ModuleNotFoundError: No module named 'config'" or ramite.MQTTManager you need to set PYTHONPATH to your current directory:

```
#export PYTHONPATH=~/SeLR:$PYTHONPATH
```


Install any missing packages in the error message

If test pass, commit the container from ssh command window

Check container id `docker container ls`, assuming it is `c3f279d17e0a`

Then commit the changes to the image of the same name

`docker commit c3f279d17e0a pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime`

To replicate the results presented in our paper, run the following bash files.
```
bash bash/fig2-3-6.sh
bash bash/fig4.sh
bash bash/fig5.sh

```



Figures 3 to 6 can be reproduced by executing the associated cells in the Jupyter notebook `Monitor.ipynb` after running the corresponding bash files. To generate Figure 2 run `Histogram.ipynb` after calling `fig2-3-6.sh`.



