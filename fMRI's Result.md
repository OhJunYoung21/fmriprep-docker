## fmriprep의 결과물

* Visual QA : fmripreprocessing의 전반적인 과정을 보여주는 .html파일을 제공한다.
* Derivatives(파생물) : fmriprep과정에서 생긴 data들을 보여준다. ex) Motion-correction이 끝난 data, SliceTiming-correction이 끝난 data 등등....
* Confounds(공변량) : 후에 잡음제거 과정에서 활용된다.


## Confounds(공변량)

사전적인 정의는 공변량이지만, 좀 더 자세하게 말하자면 어떤 특정과제가 주어졌을 때 발생하는 신호에서 잡음을 유발하는 요인들을 말한다. 뭐, 대표적으로는 head-motion correction,Slice-timing correction등이 있을 것이다.

여기서는 Confound를 머리움직임으로 인한 것과 신체 내부의 활동으로 인한 것으로 분류한다.

머리가 움직이면 당연히 BOLD signal이 발생할것이고, 그에 따른 signal은 주어지는 raw data에서 적절하게 제거해줘야 한다. 그래야 청렴한(?) data가 주어지는 것이다.

또 하나는 심장박동 또는 CSF(CerebroSpinal Fluid)으로 인해 발생하는 신호이다. 위 신호는 자극과 상관없이 발생하기 때문에 위 신호를 적절하게 제거해주는 과정이 필요하다.위 과정에서 PCA 또는 ICA 기법이 사용된다.(PCA : Principal Component Analysis, ICA: Indepent Component Analysis)

## PCA란?

## ICA란?
