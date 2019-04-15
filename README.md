# densebody_pytorch
PyTorch implementation of CloudWalk's recent paper [DenseBody](https://arxiv.org/abs/1903.10153v3).

**Note**: For most recent updates, please check out the `dev` branch.

![paper teaser](teaser/teaser.jpg)

### Network Architecture

Current experiments features 6 ConvRes blocks with stride 2 and 2 fc layers for the encoder. The structure of the decoder is symmetric with that of the encoder, with 2 fc layers following by 6 consecutive conv and upsample layers and a final `Tanh()` to get the output UV position map. The following picture showcases the result (Only 3 conv layers are drawn).

![net_arch](teaser/net_arch.png)

Training after 40 epochs yields following result:

![result](teaser/040_00999.png)

And here's the resampled body mesh shown in point cloud:

![result](teaser/recon_mesh.PNG)

### Update Notes

- Code reformating complete! Please refer to `data_utils/UV_map_generator.py` for more details.
- Thanks [Raj Advani](https://github.com/radvani) for providing new hand crafted UV maps!
- For those who already forked my project, the original code is now temporarily hosted in the `legacy` branch, and will be removed after the code reformatting is complete.

### Prerequisites
```
Windows 10 / Ubuntu 18.04
CUDA 9.0 / 9.1
Python 3.6
PyTorch 1.0.0
opencv-python
tqdm
chumpy (For converting SMPL model to basic numpy arrays)
h5py (For processing Human36m cdf annotations)
```

(Optional) Install [torch-batched-svd](https://github.com/KinglittleQ/torch-batch-svd) for speedup (Only tested under Ubuntu system).


### TODO List
- [x] Creating ground truth UV position maps for Human36m dataset.
    - [x] [20190329]() Finish UV data processing.
    - [x] [20190331]() Align SMPL mesh with input image.
    - [x] [20190404]() Data washing: Image resize to 256*256 and 2D annotation compensation.
    - [x] [20190411]() Generate and save UV position map.
        - [x] [radvani](https://github.com/radvani) Hand parsed new 3D UV data
        - [x] Validity checked with minor artifacts (see results below)
        - [x] Making UV_map generation module a separate class.
    - [x] [20190413]() Prepare ground truth UV maps for washed dataset.
    
- [x] Prepare baseline model training
    - [x] [20190414]() Network design, configs, trainer and dataloader
    - [x] [20190414]() Baseline complete with first-hand results. Something issue still needs to be addressed.
    - [ ] Testing with several new loss functions.
    - [ ] Testing with different networks.
 
- [ ] Report 3D reconstruction results.
    - [ ] Setup evaluation protocal and MPJPE-PA metrics.


### Current Progress
Finish UV texture map processing. Here's the result:

![UV_map](teaser/radvani_template_atlas.png)

Align SMPL meshes with input images. Here are some results:

![Ground Truth Image](teaser/im_gt_0.png)
![Aligned Mesh Image](teaser/im_mask_0.png)
![Generated UV map](teaser/UV_position_map_0.png)

![Ground Truth Image](teaser/im_gt_1.png)
![Aligned Mesh Image](teaser/im_mask_1.png)
![Generated UV map](teaser/UV_position_map_1.png)

Reconstruct human mesh through resampling. Here are some results.

![Original Mesh](teaser/original_mesh_0.PNG)
![Reconstructed Mesh](teaser/resampled_mesh_0.PNG)

![Original Mesh](teaser/original_mesh_1.PNG)
![Reconstructed Mesh](teaser/resampled_mesh_1.PNG)


### Citation
Please consider citing the following paper if you find this project useful.

[DenseBody: Directly Regressing Dense 3D Human Pose and Shape From a Single Color Image](https://arxiv.org/abs/1903.10153v3)

### Disclaimer
Please note that this is an unofficial implementation free for non-commercial usage only. For commercial cooperation please contact the original authors.
