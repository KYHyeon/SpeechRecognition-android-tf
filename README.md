# TensorFlow Android Speech-Recognition

### 실행 화면

<img src="https://user-images.githubusercontent.com/16751025/96371801-98250500-119e-11eb-9ef1-d3110e7b5fef.png" width=20%></img>

앱을 실행하면 현재 모델이 인식 할 수 있는 명령어들이 나옵니다. 화면이 표시되면 아래 인식할 수 있는 명령어 중 하나를 말하면 인식된 명령어가 파랗게 표시됩니다.



### 모델 파일 구조

> https://github.com/tensorflow/docs/blob/master/site/en/r1/tutorials/sequences/audio_recognition.md

* 전처리 - [tensorflow.audio.decode_wav](https://www.tensorflow.org/api_docs/python/tf/audio/decode_wav)를 이용하기 위해
  * sample rate = 16000
  * mono
  * 16-bit Signed Integer PCM

```python
import librosa
import soundfile as sf

y, sr = librosa.load({path}, sr=16000)
sf.write({new_path}, y, sr, 'PCM_16')
```

* 전처리 하기 전 파일 예시

![image-20201018235213857](https://user-images.githubusercontent.com/16751025/96371807-a3783080-119e-11eb-885c-0943a7fa55e9.png)



* 전처리 후 파일 예시

![image-20201018235223135](https://user-images.githubusercontent.com/16751025/96371808-a4a95d80-119e-11eb-8416-c423fe3821a9.png)



* 학습

```sh
python train.py \
--data_url="" \ # 웹으로 부터 다운로드 받을 url (사용하지 않을 경우 공백)
--data_dir=my_wavs \ # 학습 데이터의 위치
--wanted_words="고장진단,이상온도,원격관제,열화상카메라,..." # 인식할 단어의 종류
```



* 평가

```sh
python label_wav.py \
--graph=/tmp/my_frozen_graph.pb \
--labels=/tmp/speech_commands_train/conv_labels.txt \
--wav=/tmp/speech_dataset/left/a5d485dc_nohash_0.wav
```



* freeze - 안드로이드로 올리기 위해 그래프를 GraphDef 파일로 변환하는 과정

```sh
python freeze.py \
--start_checkpoint=/tmp/speech_commands_train/conv.ckpt-13000 \
--output_file=/tmp/my_frozen_graph.pb
```



### 안드로이드 개발 환경

- Android Studio 3.2 or later.
- Android API 21
- org.tensorflow:tensorflow-android:1.13.1 - (서버에서의 tensorflow 모델 역시 tensorflow 1.13.1에서 학습 및 테스트)



### 안드로이드 파일 구조

* java
  * Speech Activity
    * 앱을 실행시켰을 때 메인에 보일 화면
  * Recognize Commands
    * 명령어 인식 결과를 담은 자료구조
* assets
  * my_frozen_graph.pb
    * tensorflow 그래프를 freeze 하여 나온 결과물
    * 그래프의 가중치를 포함하고 있습니다.
  * conv_labels.txt
    * 모델이 인식할 수 있는 레이블의 리스트
    * 화면에 보여질 리스트



### 참고 문서

* Android : Based on https://github.com/tensorflow/tensorflow/tree/r1.13/tensorflow/examples/android
* Model : https://github.com/KYHyeon/speech_command_recognition
