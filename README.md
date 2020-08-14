# CMake_Study

> CMake 공부 문서를 작성하는 저장소입니다.

#### Reference
- [cgold](https://cgold.readthedocs.io/en/latest/overview/cmake-can.html)
- [luncliff/cmake-tutorial.md](https://gist.github.com/luncliff/6e2d4eb7ca29a0afd5b592f72b80cb5c)
- [jacking75/examples_CMake](https://github.com/jacking75/examples_CMake)

### 차례<a name="Category"></a>
- [CMake](#cmake)


## CMake란 무엇인가요?[[top](#Category)]<a name="cmake"></a>
- CMake란 메타 빌드 시스템(meta build system) 입니다. 보통 CMakeList.txt 라 이름 붙여진 텍스트 파일에 명시된 설정사항에 따라 네이티브 빌드 툴(Native build Tool) 생성하는 역할을 맡습니다.
  - 여기서 네이티브 빌드 툴(Native build Tool) 이란 특정 소프트웨어를 빌드하기 위한 도구를 명시합니다. 즉 IDE + 컴파일러라고 볼 수 있습니다. c++ 개발 환경에 경우 Visual Studio. Ninja, MakeFile, Xcode를 예로 들 수 있습니다.
  - CMake는 그 자체로 Native build Tool이 될 수 없습니다. Visual Studio 같은 IDE와는 다르게 프로그램 개발에 직접적인 도움을 주는 것은 아니며, 소스 파일을 빌드하지 않습니다. 단지 명시된 설정사항에 따라 Native Build Tool 을 생성하는 것이 CMake의 역할입니다.
  
  
#### CMake의 역할을 간단히 설명하자면
![](https://cgold.readthedocs.io/en/latest/_images/native-build.png)

익히 알다시피 다양한 IDE를 통해 소스 파일을 binary 파일로 빌드합니다. 만약 하나의 프로젝트에서 다양한 IDE를 사용하고 있다고 가정해 봅시다. 그리고 소스코드를 작성하는 과정 중 새로운 파일을 추가해야 하는 일이 생겼습니다.

![](https://cgold.readthedocs.io/en/latest/_images/native-build-add.png)

각 IDE 마다 구성 환경은 다르기 때문에, 이 경우 저희는 어쩔 수 없이 각 IDE 마다 따로 파일을 추가해야 할 것입니다. 유연성이 떨어지는 작업이라는 것을 쉽게 짐작할 수 있습니다.

![](https://cgold.readthedocs.io/en/latest/_images/generate-native-files.png)

CMake를 활용하는 경우, 프로젝트의 설정사항들을 CMakeLists.txt 에 명시합니다. CMake는 CMakeLists.txt에 명시된 사항을 확인한 뒤 여러분이 원하는 IDE 환경에 해당하는 프로젝트를 생성할 수 있습니다.

![](https://cgold.readthedocs.io/en/latest/_images/generate-native-files-add.png) 

소스 코드를 추가하는 이전 상황을 다시 봅시다. CMake를 활용하는 경우, 추가 소스 코드를 CMakeLists.txt에 명시하면 더 추가적인 작업은 필요 없습니다. CMake가 최신화된 소스코드를 확인해서 각 IDE에 맞는 프로젝트를 생성해 줄 테니까요.

- 한 가지 강조할 점은, IDE 환경에서 소스 파일을 추가하는 작업과 CMakeLists.txt에 추가 소스코드를 명시하는 작업 두 가지는 분명히 다른 작업이라는 것입니다. CMake는 CMakeLists.txt에 명시된 파일만 확인할 수 있으니 IDE에서 파일을 추가한 뒤에 CMakeLists.txt에 명시하지 않으면 CMake는 변경사항을 인식하지 못한다는 겁니다.
![](https://cgold.readthedocs.io/en/latest/_images/bad-workflow.png)
![](https://cgold.readthedocs.io/en/latest/_images/good-workflow.png)

- 추가적으로 IDE 에서 제공하는 설정들과 CMake에서 작성할 수 있는 설정사항들은 항상 호환되지는 않는다는 점도 기억합시다.
