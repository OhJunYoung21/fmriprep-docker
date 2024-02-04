## fMRI-preprocessing-pipeline

위 레파지토리에서는 cocoan's lab에서의 fMRI preprocessing pipeline을 정리하였습니다.

먼저 설치해줘야 하는 소프트웨어는 아래와 같습니다.

### Dependency

1. Canlab Core: [https://github.com/canlab/CanlabCore](https://github.com/canlab/CanlabCore)
2. dicm2nii.m: ([link](https://www.mathworks.com/matlabcentral/fileexchange/42997-dicom-to-nifti-converter--nifti-tool-and-viewer)): We modified the original toolbox a little bit to make the output data fully BIDS-compatible. For this reason, please use the dicm2nii toolbox in our repository (in /external), instead of the original one. 
3. FSL: [https://fsl.fmrib.ox.ac.uk](https://fsl.fmrib.ox.ac.uk)
4. SPM12: [http://www.fil.ion.ucl.ac.uk/spm/software/spm12](http://www.fil.ion.ucl.ac.uk/spm/software/spm12)
5. ICA-AROMA: [https://github.com/rhr-pruim/ICA-AROMA](https://github.com/rhr-pruim/ICA-AROMA)
6. Anaconda: [https://www.anaconda.com/download/#macos](https://www.anaconda.com/download/#macos)
