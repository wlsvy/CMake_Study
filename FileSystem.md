# Cmake FileSystem 명령어

```
file(GLOB <variable>
     [LIST_DIRECTORIES true|false] [RELATIVE <path>] [CONFIGURE_DEPENDS]
     [<globbing-expressions>...])
file(GLOB_RECURSE <variable> [FOLLOW_SYMLINKS]
     [LIST_DIRECTORIES true|false] [RELATIVE <path>] [CONFIGURE_DEPENDS]
     [<globbing-expressions>...])
```

- globbing 이란 임의의 문자기호를 포함하는 파일이름을 특정 저장소/서버/디렉토리 안에서 찾아내는 과정이라고 합니다.

- 위의 명령어에서 GLOB 은 특정 디렉토리의 파일들을 대상으로, GLOB_RECURSE 는 해당 경로내 하위 디렉토리의 파일까지 대상으로 합니다.
- GLOB을 사용한다면 cmake빌드가 된 프로젝트에 대해서, 디렉토리 안에 파일을 추가/삭제할 때 해당 파일이 생성/삭제되었다는 것을 cmake에게 알려줄 방법이 없다는 것이 단점입니다. (다시 cmake빌드를 하지 않는 이상)

#### Reference
- [Cmake : File](https://cmake.org/cmake/help/latest/command/file.html#filesystem)
