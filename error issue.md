## Error issue

~~~unix
nipype.pipeline.engine.nodes.NodeExecutionError: Exception raised while executing Node _inu_n40.
~~~

위 같은 에러 메세지가 관찰 되었다. 해당 오류는 neurostar에 조회한 결과 메모리 할당 문제인 것을 밝혀져 메모리를 좀 더 여유롭게 할당하면 오류없이 돌아갈 듯 하다.
