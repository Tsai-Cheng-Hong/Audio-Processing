<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/us/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/us/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/us/">Creative Commons Attribution-NonCommercial-ShareAlike 3.0 United States License</a>.

# Transform-average-concatenate (TAC) for end-to-end microphone permutation and number invariant multi-channel speech separation

This repository provides the model implementation and dataset generation scripts for the paper ["End-to-end Microphone Permutation and Number Invariant Multi-channel Speech Separation"](https://arxiv.org/abs/1910.14104) by Yi Luo, Zhuo Chen, Nima Mesgarani and Takuya Yoshioka. The paper introduces ***transform-average-concatenate (TAC)***, a simple module to allow end-to-end multi-channel separation systems to be invariant to microphone permutation (indexing) and number. Although designed for ad-hoc array configuration, TAC also provides significant performance improvement in fixed geometry microphone configuration, showing that it can serve as a general design paradigm for end-to-end multi-channel processing systems.

## Model

We implement TAC in the framework of ***filter-and-sum network (FaSNet)***, a recently proposed multi-channel speech separation model operated in time-domain. FaSNet is a neural beamformer that performs the standard filter-and-sum beamforming in time domain, while the beamforming coefficients are estimated by a neural network in an end-to-end fashion. For details please refer to the original paper: ["FaSNet: Low-latency Adaptive Beamforming for Multi-microphone Audio Processing"](https://arxiv.org/abs/1909.13387).

In this paper we make two main modifications to the original FaSNet:
1) Instead of the original two-stage architecture, we change it into a single-stage architecture.
2) TAC is applied throughout the filter estimation module to synchronize the information in different microphones and allow the model to perform *global* decision while estimating the filter coeffients.

The figure below shows different designs of FaSNet models.
![](https://github.com/yluo42/TAC/blob/master/flowchart.png)

The building blocks for the filter estimation modules are based on ***dual-path RNNs (DPRNNs)***, a simple yet effective method for organizing RNN layers to allow successful modeling of extremely long sequential data. For details about DPRNN please refer to ["Dual-path RNN: efficient long sequence modeling for time-domain single-channel speech separation"](https://arxiv.org/abs/1910.06379). The implementation of DPRNN, as well as the combination of DPRNN and TAC, can be found in [*utility/models*](https://github.com/yluo42/TAC/blob/master/utility/models.py).

## Dataset

The evaluation of the model is on both ad-hoc array and fixed geometry array configurations. We simulate two datasets on the public available Librispeech corpus. For data generation please refer to the *data* folder.
