# ContextFlow: Context-Aware Lightweight Optical Flow CNN for Optical Flow Estimation

This is the context-aware implementation of the lightweight CNN LiteFlowNet as our CS484 Final Project.

### Group: [Efe Acer](https://github.com/efeacer), [Kuluhan Binici](https://github.com/kuluhan), [Mert Duman](https://github.com/MertDuman)

## Novelties
- After calculating the cost volumes and estimating the optical flow, a context network is utilized to refine the estimated flow.
- Introduce additional error terms to the Charbonnier Loss function ($\rho(x) = (x^2 + \epsilon^2)^q$) ??
- Unsupervised learning??

## Dataset
We use the [MPI Sintel Dataset](http://sintel.is.tue.mpg.de/) to train our network. Since it is a synthetic dataset, it is designed to include image sequences with motion blur, long-range motion and occluded pixels. The design addresses some of the limitations of current optical flow techniques and creates a challenge.

![](images/sample.gif)

## Acknowledgement
We were inspired and influenced by PWC-Net and LiteFlowNet in design and code, we thank the authors for their hard work.
