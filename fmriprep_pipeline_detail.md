## 🧠fmriprep_pipeline_detail🧠

여기서는 fmriprep이 어떤 순서로 이뤄지며, 각 단계가 수행되는 이유(필자의 주관 다소 개입)과 원리에 대해서 간략하게 다뤄볼예정이다.

### Preprocessing structural MRI

해부학적 이미지는 주로 t1w이미지로 제공된다. 맨 처음 fmriprep에서는 주어지는 t1w가 RAS 좌표계를 사용하도록 한다.RAS = (R:Right , A:Anterior, S:Superior)

만일 주어지는 이미지가 LPS(RAS와 반대 좌표계)를 쓰고 있었다면 이를 RAS좌표로 바꾸는 것이다. 이 부분도 이해가 잘 안돼서 자세한 예시를 들자면, 만일 LPS좌표계에서 어떤 부위의 좌표가 (10,20,30)이었다면, RAS기준으로 해당 좌표는 (10,-20,-30)이다.
즉, 모든 좌표를 RAS의 방식으로 표현하라는 것이다. 무슨 과학적인 원리가 숨어있는 것은 아니다. 단순히 RAS는 국제 표준좌표계이며, 개인간의 비교를 원활하게 하기 위해서 진행한다고 보면 될 것이다.

또한 주어지는 데이터의 voxel 단위가 2mm^3라면, 1mm^3으로 바꿔준다. 이 또한 규격을 맞춰서 비교를 원활하게 하기 위함이다.

그 다음에는 아래의 3가지 과정이 진행된다.

* Brain Extraction
* Brain Tissue Segmentation
* Spatial Normalization

---

### Brain Extraction

위 과정은 단순하게 생각해서, 주어지는 뇌 영상 데이터에서 두개골부분을 제거한다고 보면 된다. fmriprep에서는 antsBrainExtraction.sh를 사용하며, FSL에서는 BET를 사용하여 진행한다.

### Brain Tissue Segmentation

위 과정은 brain mask를 만들고, 뇌 마스크를 토대로 뇌의 특정 영역을 구별해주는 것이다. 뇌 마스크는 여러가지 방법으로 만들 수 있는데, 기존의 해부학적 지식을 토대로 만들 수도 있지만, 딥러닝기술을 적용시켜 컴퓨터가 스스로 raw data를 보고 부위별로 구별해낼 수도 있다.

결과물은 아래의 사진과 같다.
![sub-01_dseg](https://github.com/OhJunYoung21/fmriprep-docker/assets/81908471/d9d14545-74ad-467e-907f-b02f0449939c)

### Spatial Normalization(공간정규화)
---
### BOLD preprocessing
---
BOLD preprocessing이란, fMRI결과 주어지는 BOLD signal에서 잡음을 제거하는 과정이다. task와 연관이 없는 BOLD signal이 있을 수 있는데, 위 같은 경우를 고려하여 BOLD signal을 정제하는 과정을 말한다. 
