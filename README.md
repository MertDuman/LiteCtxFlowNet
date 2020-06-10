# ContextFlow: Context-Aware Lightweight Optical Flow CNN for Optical Flow Estimation

This is the context-aware implementation of the lightweight CNN LiteFlowNet as our CS484 Final Project.

### Group: [Efe Acer](https://github.com/efeacer), [Kuluhan Binici](https://github.com/kuluhan), [Mert Duman](https://github.com/MertDuman)

## Novelties
- After calculating the cost volumes and estimating the optical flow, a context network is utilized to refine the estimated flow.
- Introduce additional error terms to the Charbonnier Loss function (<img src="/tex/5bed07659f226b5a24730c6ffa8700e4.svg?invert_in_darkmode&sanitize=true" align=middle width=122.72769794999998pt height=26.76175259999998pt/>) ??
- Unsupervised learning??

## Dataset
We use the [MPI Sintel Dataset](http://sintel.is.tue.mpg.de/) to train our network. Since it is a synthetic dataset, it is designed to include image sequences with motion blur, long-range motion and occluded pixels. The design addresses some of the limitations of current optical flow techniques and creates a challenge.

![](images/combined.gif)

## Results
<table>
<thead>
<tr>
<th align="center"></th>
<th align="center">KITTI12 Testing Set (Out-Noc)</th>
<th align="center">KITTI15 Testing Set (Fl-all)</th>
<th align="center">Model Size (M)</th>
</tr>
<tr>
<td align="center">FlowNet2 (CVPR17)</td>
<td align="center">4.82%</td>
<td align="center">10.41%</td>
<td align="center">162.49</td>
<tr>
<td align="center">PWC-Net (CVPR18)</td>
<td align="center">4.22%</td>
<td align="center">9.60%</td>
<td align="center">8.75</td>
</tr>  
<tr>
<td align="center"><strong>LiteFlowNet (CVPR18)</strong></td>
<td align="center"><strong>3.27%</strong></td>
<td align="center"><strong>9.38%</strong></td>
<td align="center"><strong>5.37</strong></td>
</tr>    
</tbody></table>

## Build Caffe
- Navigate to Caffe folder, you need to modify Makefile.config based on your GPU.
- run 'make -j8 pycaffe tools' inside the Caffe folder to build the Caffe model.

## Training
- Inside the Caffe->Data folder. You can download the sintel dataset by running download_sintel.sh.
- We also provide a sample file_loc_abs.list file that lists all the names of the training images.
- Edit make-lmdbs.train.sh to direct to your .list file and choose the name of the output .lmdb file name.
- execute the above shell script.
- Navigate to Caffe->models->New folder.
- Modify train.prototxt file as follows:
    - under data_param {}, modify source: to point to your _lmdb datasets.
- Run './train.py -gpu 0 2>&1 | tee ./log.txt' to start training.
- OR Run './train.py -gpu 0 -weights <path_to_your_caffemodel> 2>&1 | tee ./log.txt' to start training from a checkpoint.

## Inference
- Navigate to Caffe->models->trained folder.
- Add your own caffemodel to that folder and then rename your model to "liteflownet.caffemodel".
- Navigate to Caffe->models->Testing folder.
- Link the build by running 'ln -s ../../build/tools bin'.
- Modify img1_pathList falan filan onlar frame1 frame2
- Run './test_batch.py img1_pathList.txt img2_pathList.txt results'

## Notes
- Caffe->models->new->train.prototxt is our own trained model structure.
- Caffe->models->new->training->context_flow.caffemodel is our own trained model.
- Caffe->models->testing->deploy.prototxt is our own structure definition for inference.
- Caffe->models->trained->liteflownet.caffemodel is our own model but renamed as liteflownet to use for inference.

## Acknowledgement
We were inspired and influenced by [PWC-Net](https://github.com/NVlabs/PWC-Net) and [LiteFlowNet](https://github.com/twhui/LiteFlowNet) in design and code, we thank the authors for their hard work.

