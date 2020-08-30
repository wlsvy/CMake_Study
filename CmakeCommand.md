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

# 프로젝트 컴파일러 경고 다루기

- 아래는 MSVC 환경에서 특정 경고(C26495, C6001)를 사용하지 않도록 설정하는 예시입니다.
  - 변수 `target` 은 현재 프로젝트 이름을 저장합니다.

```console
if(MSVC)
target_compile_options(${target} PUBLIC 
    /wd6001
    /wd26495
)
endif()
```

#### Reference
- [Stackoverflow : how-to-disable-specific-warning-inherited-from-parent-in-visual-studio](https://stackoverflow.com/questions/41205725/how-to-disable-specific-warning-inherited-from-parent-in-visual-studio)
- [Microsoft : compiler warning option](https://docs.microsoft.com/en-us/previous-versions/thxezb7y(v=vs.140)?redirectedfrom=MSDN)

# Copy File

- `file` , `configure_file`, `add_custom_command` 명령어를 활용해서 cmake 빌드 시 특정 디렉토리의 파일을 복사할 수 있습니다.
  - `file` 명령어를 사용하는 경우, cmake의 configuration 단계에서만 파일을 복사합니다. 다른 두 가지 명령어를 활용한다면 기존 파일이 수정되었을 경우, cmake가 이를 추적하여 복사를 다시 수행해주는 장점이 있으니 `file` 보다는 `configure_file`, `add_custom_command`를 활용하는 것이 권장되고 있습니다.
  
 ```
 # Copy DLL
configure_file(
    ${PRECOMPILED_LIBRARY_DIRECTORY}/x64/Debug/assimp-vc140-mt.dll 
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Debug/assimp-vc140-mt.dll 
COPYONLY)
configure_file(
    ${PRECOMPILED_LIBRARY_DIRECTORY}/x64/Release/assimp-vc140-mt.dll 
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/Release/assimp-vc140-mt.dll 
COPYONLY)
 ```

#### Reference
- [stackoverflow : copy-file-from-source-directory-to-binary-directory-using-cmake](https://stackoverflow.com/questions/34799916/copy-file-from-source-directory-to-binary-directory-using-cmake/42397802)
- [cmake : add_custom_command](https://cmake.org/cmake/help/v2.8.10/cmake.html#command:add_custom_command)
- [cmake : configure_file](https://cmake.org/cmake/help/latest/command/configure_file.html)
