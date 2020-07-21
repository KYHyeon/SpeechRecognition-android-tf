# TensorFlow Android Speech-Recognition

* Android : Based on https://github.com/tensorflow/tensorflow/tree/r1.13/tensorflow/examples/android
* Model : https://github.com/KYHyeon/speech_command_recognition

Requirements
---
* Android Studio 3.2 or later.
* Android API 21
* org.tensorflow:tensorflow-android:1.13.1 - (서버에서의 tensorflow 모델 역시 tensorflow 1.13.1에서 학습 및 테스트)

Images
---
<img src="/docs/init.png" width="20%">


Running the app
---
1. 깃을 통해 repo를 클론 받는다.
```git clone https://github.com/KYHyeon/SpeechRecognition-android-tf.git```
2. android studio를 실행하여 gradle sync를 통해 의존성을 다운받는다.
3. 모바일에서 TF Speech를 실행하여 결과를 확인한다.

Code
---
* [Main Activity](https://github.com/KYHyeon/SpeechRecognition-android-tf/blob/master/src/org/tensorflow/demo/SpeechActivity.java)
* Assets
  - [my_frozen_graph.pb](https://github.com/KYHyeon/SpeechRecognition-android-tf/blob/master/assets/my_frozen_graph.pb): 커스텀 모델의 그래프를 고정(freeze)한 파일
  - [conv_labels.txt](https://github.com/KYHyeon/SpeechRecognition-android-tf/blob/master/assets/conv_labels.txt): 인식 대상 단어의 종류 & 화면에 표시될 단어의 종류