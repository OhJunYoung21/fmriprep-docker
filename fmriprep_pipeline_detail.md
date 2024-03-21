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
## BOLD preprocessing

BOLD preprocessing이란, fMRI결과 주어지는 BOLD signal에서 잡음을 제거하는 과정이다. task와 연관이 없는 BOLD signal이 있을 수 있는데, 위 같은 경우를 고려하여 BOLD signal을 정제하는 과정을 말한다. 

BOLD preprocessing에는 HeadMotion correction, SliceTiming correction등이 사용된다. Head motion correction이 이뤄지려면 기준이 되는 뇌의 이미지가 필요하다.

기준이 되는 뇌의 이미지가 있어야 해당 이미지에서 많이 벗어난 이미지를 교정할 수 있기 떄문이다. 이해하기 힙들다면 '틀'이 되는 이미지를 먼저 생성해야 한다고 보면 될것이다.

### BOLD reference image estimation

위 부분은 좀 공부하기 힘들었다. reference image가 무엇인지 몰랐기 때문에 아마도 이해하기 힘들었을 것이라 생각한다. 또한 estimation이 정확히 무엇인지 몰랐기에 더 힘들었을 것이다.

공식문서에 보면 아래와 같은 문구가 나온다.

~~~MarkDown
This workflow estimates a reference image for a BOLD series as follows
: When T1-saturation effects (“dummy scans” or non-steady state volumes) are detected,
they are averaged and used as reference due to their superior tissue contrast.
~~~

위 말은 물론 사전적으로 해석할 수도 있겠지만, 내 식대로 설명하자면 fMRI 촬영초기에는 조직이완으로 인해 BOLD signal이 제대로 관측되지 않는다(왜곡된다). 그렇지만 해부학적인 부분은 영향을 받지 않기 때문에 해당 이미지를 reference 이미지로 삼는 것이다. 좀 더 직관적으로 설명하자면 fMRI 극 초기에 촬영된 영상을 기준점으로 삼고, 시간에 따라 두개골의 움직임이 감지되면 reference이미지를 기준으로 다시 두개골의 위치를 조정하는 것이다. 마치 우리가 줄을 설때 맨 앞사람을 기준으로 삼고 줄을 맞추는 것과 동일한 원리이다.
