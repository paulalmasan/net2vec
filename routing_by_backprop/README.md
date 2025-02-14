# routing_by_backprop

Routing By Backprop (RBB) is a Traffic Engineering (TE) method based on Graph Neural Networks (GNN) and differentiable programming. 
Thanks to its internal GNN model, RBB builds an end-to-end differentiable function of the target TE problem (_MinMaxLoad_), 
which enables fast TE optimization via gradient descent. 
In our evaluation we show the potential of RBB to optimize OSPF (~25% of 
improvement w.r.t. default OSPF configurations). 
Likewise, we test the potential of RBB as an initializer of computationally-expensive TE solvers, 
showing promising prospects for accelerating such type of solvers and achieving efficient online 
TE optimization.

This repository contain code used in the numerical experiments, and allow for reproductioin of our results.

# Train

First we need to train the model for appropriate large dataset.

```shell
python3 python/sp.py --train_graphs=10 --test_graphs=2 --checkpoint_steps=2
```

# Optimize

Once the model is trained, it can be used for network optimization.
Below is the example for nsf network topology.

```shell
	mkdir -p out/$@
	PYTHONPATH=baselines:${PYTHONPATH} python3 python/optimize_sp.py \
		--num_opt 5 \
		--report out/$@/opt.csv \
		--num_sgd 1 \
		--nopmap

```

**If you decide to apply the concepts presented or base on the provided code, please do refer our paper.**

```
@misc{https://doi.org/10.48550/arxiv.2209.10380,
  doi = {10.48550/ARXIV.2209.10380},
  
  url = {https://arxiv.org/abs/2209.10380},
  
  author = {Rusek, Krzysztof and Almasan, Paul and Suárez-Varela, José and Chołda, Piotr and Barlet-Ros, Pere and Cabellos-Aparicio, Albert},
  
  keywords = {Networking and Internet Architecture (cs.NI), FOS: Computer and information sciences, FOS: Computer and information sciences},
  
  title = {Fast Traffic Engineering by Gradient Descent with Learned Differentiable Routing},
  
  publisher = {arXiv},
  
  year = {2022},
  
  copyright = {arXiv.org perpetual, non-exclusive license}
}

```

