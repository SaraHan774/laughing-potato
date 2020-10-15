# Lab 0 Writeup

My name: Sara Gahee Han

- Optional: I had unexpected difficulty with: `cmake ..` 을 하고 나니, g++ 버전에 문제가 있었다. g++ 8 을 다운받아서 update-alternative 를 하였는데도 바뀐 버전이 적용이 되지 않았다. CMake 파일이 어떤 버전을 인식하는지 알아보고자 message() 로 버전을 찍어보니 이전의 7.5.0 버전이 나왔다. 터미널을 껐다가 켜봐도 적용이 되지 않았는데, 결국 CMakeCache 파일이 문제라는 것을 알아냈다. Cache 를 삭제하니 바로 빌드가 성공했다.

- Optional: I think you could make this lab better by: [describe]

- Optional: I was surprised by: [describe]

- Optional: I'm not sure about: [describe]

---

### 과제 명세

#### 1. apps 폴더 밑의 webget.cc 에 비어있는 코드 작성하기.

- 힌트

  - HTTP 의 라인은 "\r\n"으로 끝나야 한다.
  - Connection : close 를 요청에 보내는 것을 잊지 말 것.
  - 10줄 정도의 코드면 충분함.

- 컴파일 `make`

  - 에러 메시지가 나오면 코드를 고쳐야함.

- 마감 기한 : 10월 14일 ~ 10월 22일 (cs144 의 과제 기간을 따라서 8일로 설정)

- 테스트 결과 화면
  <img src="./webget-test-result.jpg" alt="webget-test-result" style="zoom: 50%;" />

#### 2. An in-memory reliable byte stream

- byte_stream.hh 와 byte_stream.cc 파일의 인터페이스를 구현하라.

- 마감 기한 : 10월 15일 ~ 10월 30일 (cs144 의 과제 기간을 따라서 14일로 설정)

- **과제 상세설명**

  - reliable byte stream 에 대한 추상화 레이어를 제공하는 객체를 인메모리로 작성할 것. byte들은 input 사이드에 쓰여지고, output 쪽에서 이를 읽을 수 있다. 바이트스트림은 finite 하다. 즉, 쓰는 쪽에서 input 을 끝낼 수 있으며, 더 이상 바이트들이 쓰여지지 못하도록 할 수 있다. 읽는 쪽에서 스트림을 끝까지 읽으면 EOF 에 도달할 것이며, 더 이상 바이트를 읽지 못하게 된다.

  - 당신의 바이트스트림은 flow-control 되어야 한다. 이는 메모리 소비를 제한하기 위함이다. 객체는 특정한 capacity 값으로 초기화 된다. 이는 특점 시점에 얼만큼의 바이트를 메모리에 저장할 것인가에 대한 용량이다. 바이트 스트림은 writer 가 특정 시점에 얼만큼의 바이트를 쓸 수 있는지를 제한하여 용량을 넘지 못하도록 한다. 읽는 쪽에서 바이트를 읽고 스트림에서 drain 하면, 라이터는 더 쓸 수 있게 된다.

  - 당신의 바이트스트림은 single thread 에서 사용된다. locking, race condition 에 대해서는 고려하지 않는다.

  - capacity 는 아직 읽혀지지 않았고 메모리에 저장되어 있는 바이트스트림에 대한 용량이다. 실제로 바이트스트림은 작위적인 크기를 가질 수 있다. 1바이트의 객체더라도, 테라바이트 이상의 stream 을 carry 할 수 있다. (쓰는 쪽에서 한 번에 1바이트만 쓰고, 다시 1바이트를 쓰기 전에 이를 읽어간다면.)
