## 사용방법

지금부터는 fmriprep-docker를 어떻게 사용하는지에 대해서 다뤄볼 것입니다.

입력하는 코드는 아래와 같습니다.

~~~unix
fmriprep-docker <bids_dir><output_dir><analysis_level>
~~~

* bids_dir : BIDS_validated된 데이터가 들어있는 폴더의 경로를 입력합니다. ex)  $HOME/user/bids
* output_dir : 결과물이 저장될 폴더를 지정합니다. ex) $HOME/user/bids/result
* analysis_level : default값으로 participant를 입력합니다.








