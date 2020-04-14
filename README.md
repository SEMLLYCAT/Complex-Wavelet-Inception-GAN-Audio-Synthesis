# Complex-Wavelet-Inception-GAN-Audio-Synthesis
This is a github project improving the learning representation of waveform signal such as audio.  
Our discussion focuses on the High Fidelity (HiFi) Audio Synthesis, which can be applied in various applications such as TTS and music generation. The previous works including Tacotron2, GANSynth, Wavenet have demonstrated very high quality simulations of sound sources, which are nearly undistinguishable. However, in the field of HiFi music and/or HiFi speech synthesis, we are still interested in higher-resolution audio representation to push the modeling of fine-grained waveform signals even further. 
## Why is waveform data so intractable in general?
Through previous scientific reports, we already know that 1D waveform data can hardly be modelled by 1D convolutional layers or fully connected layers. The spectral properties of sounds are non-local, as waveform audio is a complex mixture of various fundamental waves and their harmonics. Unlike image, audio oscillates up and down, which reflects not only amplitude but also phase.
  
Because the direct modeling of waveform data is tough, many studies choose to model the intermediate spectrogram, a two-dimensional image-like time-frequency product of short time Fourier transform. However, because the horizontal axis means time and the vertical axis means frequency, audio does not apply translation invariance. Also, as the human hearing is very sensitive, even tiny little noise can cause very uncomfortable experience to ears. The current audio generation is limited by the reconstruction algorithm of waveform data from spectrogram, the resolution limitation cause by time-frequency trade-off, and also the information loss caused by STFT.
## Previous works focus on imperfect STFT-spectrogram
In early 21 centuries, many studies have reported that the mel-scaled STFT spectrogram is the most effective representation for audio classification, which outperformed many other time-frequency analysis tools such as CQT, MFCC, CWT, etc. Just recently, deep learning audio synthesis have all demonstrated that mel-scaled spectrogram with advantages in seperating harmonics and adapting human ears have successfully brings about high-fidelity audio/speech synthesis. People have overcome the problems of audio reconstruction by IF learning (github.com/tensorflow/magenta/tree/master/magenta/models/gansynth), Phase Gradient Heap Integration (https://tifgan.github.io/#S-E), neural inverse transform (github.com/descriptinc/melgan-neurips) and Wavenet-based vocoder (https://github.com/NVIDIA/tacotron2). Thanks to these studies, high-fidelity audio/speech synthesis is no longer a dream. However, from the signal processing theory, we know that STFT is not a perfect solution for audio representation. 
  
## Idea1. Complex-valued convolution for complex spectrogram
The learning representation of complex spectrogram can avoid scattering the information of phase. The complex spectrogram, however, can hardly be processed by real-valued neural network. Introducing the architecture of DEEP COMPLEX NETWORKS (Chiheb Trabelsi et al.), we learned complex spectrogram directly. This, however, does not allow the modeling of logrithmic spectrogram, which severely restricts precision.
## idea2. Wavelet transform to replace short time Fourier Transform
The short time Fourier Transform is not flexible and fine enough to filter audio features at different frequency scales. The modeling of wavelet spectrogram does not sacrifice the time resolution as STFT transformation, but instead seperate the signal mixture into different frequencies. This is potentially eligible to extract finer signal features, but also increases algorithm complexity/scale.
## Idea3. Inception generator to capture features at different frequency scales
Inspired by inception network, we designed a generator architecture that provides 1D convolution filters of flexible sizes to capture audio features at different frequency scales. Audio signal is a mixture of various foundamental waves and harmonic waves. Different foundamental waves are at different frequency ranges, and their harmonic waves are at their multiple frequencies. All these together are too complicated for a single-sized convolution to process. Therefore, we proposed to use multi-sized filters to generate waveform audio signal at first layer, just like an inversed version inception network. This might sounds plausible intuitively but does not come to a good result as experiment has shown.
## Idea4. Adaptive complex freqency domain kernels instead of time domain
Although audio signal in time domain is twisted, the complex freqency domain has reflected signal's core features. If we can seperate signals at different frequency ranges by adaptive freqency domain kernels, the audio will no longer be mixed. We do prove that this approach is helpful; however, this new layer is still not proved more efficient than convolutional layers. This idea direction is very interesting because it nearly touches the core of deep learning representation. Although the current experiments are not proving its feasibility, its potential can not be denied. More research may require in this direction.
## What is next?
We are working in progress to experiment and currently the idea2 seems most expecting. We have gotten some thriving results to show that idea2 does boost audio fidelity and can surpass the state-of-the-art models mentioned above if computation complexity is not concerned. 
## Author Affiliation Information
Yingtao Luo, Siqi Sun, Kun He, et al., Huazhong University of Science and Technology, et al.
