# Deep RL for traffic signal control

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repo implements start-of-the-art mutli-agent (decentralized) deep RL algorithms for large-scale traffic signal control in SUMO-simulated environments.

Available cooperation levels:
* Centralized: a global agent that makes global control w/ global observation, reward.
* Decentralized: multiple local agents that make local control independently w/ neighborhood information sharing.

Available NN layers:
Fully-connected, LSTM.

Available algorithms:
IQL, IA2C, IA2C with stabilization (called MA2C).

Available environments:
* A 6-intersection benchmark traffic network. [Ye, Bao-Lin, et al. "A hierarchical model predictive control approach for signal splits optimization in large-scale urban road networks." IEEE Transactions on Intelligent Transportation Systems 17.8 (2016): 2182-2192.](https://ieeexplore.ieee.org/abstract/document/7406703/)
* A 5X5 traffic grid. [Chu, Tianshu, Shuhui Qu, and Jie Wang. "Large-scale traffic grid signal control with regional reinforcement learning." American Control Conference (ACC), 2016. IEEE, 2016.](https://ieeexplore.ieee.org/abstract/document/7525014/)
* A modified Monaco traffic network with 30 signalized intersections. [L. Codeca, J. Härri, "Monaco SUMO Traffic (MoST) Scenario: A 3D Mobility Scenario for Cooperative ITS" SUMO 2018, SUMO User Conference, Simulating Autonomous and Intermodal Transport Systems May 14-16, 2018, Berlin, Germany.](http://www.eurecom.fr/en/publication/5527/download/comsys-publi-5527.pdf) ([code](https://github.com/lcodeca/MoSTScenario))


## Requirements
* Python3
* [Tensorflow](http://www.tensorflow.org/install)
* [SUMO](http://sumo.dlr.de/wiki/Installing)

## Usages
First define all hyperparameters in a config file under `[config_dir]`, and create the base directory of experiements `[base_dir]`. Before the training, SUMO xml files have to be generated by calling `build_file.py` under `[environment_dir]/data/`.

To train a new agent, run
~~~
python3 main.py --base-dir [base_dir] train --config-dir [config_dir] --test-mode no_test
~~~
`no_test` is suggested, since it may slow down the training speed.

To access tensorboard during training, run
~~~
tensorboard --logdir=[base_dir]/log
~~~

To evaluate and compare trained agents, run
~~~
python3 main.py --base-dir [base_dir] evaluate --agents [agent names] --evaluate-seeds [seeds]
~~~
Evaluation data will be output to `[base_dir]/eva_data`, and make sure evaluation seeds are different from those used in training.

