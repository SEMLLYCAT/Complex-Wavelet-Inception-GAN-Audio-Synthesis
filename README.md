# Complex-Wavelet-Inception-GAN-Audio-Synthesis
The adversarial audio synthesis started from the work of Chris Donahua et al.(https://github.com/chrisdonahue/wavegan), which aimed at the unsupervised audio synthesis. Following studies have used various strategies to improve the fidelity of generated audio, such as Phase Gradient Heap Integration introduced by Andr´es Maraﬁoti et al.(https://tifgan.github.io/#S-E), IF-Phase learning proposed by Jesse Engel et al.(https://github.com/tensorflow/magenta/tree/master/magenta/models/gansynth), inverse transform of Melspectrogram to raw wave audio (https://github.com/descriptinc/melgan-neurips), etc. Using different approaches, we explored ways to improve the fidelity of generated audio, including complex-valued convolution, wavelet transform, and inception generator.
## 1. Complex-valued convolution for complex spectrogram
The learning representation of complex spectrogram can avoid scattering the information of phase. The complex spectrogram, however, can hardly be modeled by real-valued neural network. Introducing the architecture of DEEP COMPLEX NETWORKS (Chiheb Trabelsi et al.), we learned complex spectrogram directly. This bypasses the loss of phase information when merely learning the magnitude of spectrogram.
## 2. Wavelet transform to replace short time Fourier Transform
The short time Fourier Transform is not flexible enough to filter audio features at different frequency scales. This is not a significant improvement in experiments, since the major problems in unsupervised audio synthesis are phase recovery and the quality of generation.
## 3. Complex-valued convolution for complex spectrogram
