##Electron으로 윈도우 웹앱 개발하기##

###reference###
- [electron으로-웹-앱-만들듯-데스크톱-앱-만들기]( http://developer.dramancompany.com/2015/12/electron%EC%9C%BC%EB%A1%9C-%EC%9B%B9-%EC%95%B1-%EB%A7%8C%EB%93%A4%EB%93%AF-%EB%8D%B0%EC%8A%A4%ED%81%AC%ED%86%B1-%EC%95%B1-%EB%A7%8C%EB%93%A4%EA%B8%B0)
- [electron 한글 튜토리얼 - 시작하기](https://github.com/electron/electron/blob/master/docs-translations/ko-KR/tutorial/quick-start.md)


1. nodejs 설치
- nodejs.org에서 installer 다운로드 및 설치

Java 사용하기 (아래는 윈도우에서 해당됨)
- python 필요함
- python 설치 후 path 지정할 것
- window 종속 있음
    - .Net Framework 2.0 SDK 혹은 Visual Studio 2005 필요함
    - The Windows 8.1 SDK 필요함
    -
C:\dev\nodejs>npm install java
-
> java@0.7.2 install C:\dev\nodejs\node_modules\java
> node-gyp rebuild


C:\dev\nodejs\node_modules\java>if not defined npm_config_node_gyp (node "C:\dev\nodejs\node_modules\npm\bin\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "" rebuild )
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
gyp ERR! stack     at failNoPython (C:\dev\nodejs\node_modules\npm\node_modules\node-gyp\lib\configure.js:401:14)
gyp ERR! stack     at C:\dev\nodejs\node_modules\npm\node_modules\node-gyp\lib\configure.js:356:11
gyp ERR! stack     at FSReqWrap.oncomplete (fs.js:82:15)
gyp ERR! System Windows_NT 10.0.10586
gyp ERR! command "C:\\dev\\nodejs\\node.exe" "C:\\dev\\nodejs\\node_modules\\npm\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebuild"
gyp ERR! cwd C:\dev\nodejs\node_modules\java
gyp ERR! node -v v4.4.5
gyp ERR! node-gyp -v v3.3.1
gyp ERR! not ok
npm ERR! Windows_NT 10.0.10586
npm ERR! argv "C:\\dev\\nodejs\\node.exe" "C:\\dev\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install" "java"
npm ERR! node v4.4.5
npm ERR! npm  v2.15.5
npm ERR! code ELIFECYCLE

npm ERR! java@0.7.2 install: `node-gyp rebuild`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the java@0.7.2 install script 'node-gyp rebuild'.
npm ERR! This is most likely a problem with the java package,
npm ERR! not with npm itself.
npm ERR! Tell the author that this fails on your system:
npm ERR!     node-gyp rebuild
npm ERR! You can get information on how to open an issue for this project with:
npm ERR!     npm bugs java
npm ERR! Or if that isn't available, you can get their info via:
npm ERR!
npm ERR!     npm owner ls java
npm ERR! There is likely additional logging output above.

npm ERR! Please include the following file with any support request:
npm ERR!     C:\dev\nodejs\npm-debug.log




#### VS2015 설치 후 ####
C:\dev\nodejs\node_modules\java>if not defined npm_config_node_gyp (node "C:\dev\nodejs\node_modules\npm\bin\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "" rebuild )
이 솔루션의 프로젝트를 한 번에 하나씩 빌드합니다. 병렬 빌드를 사용하려면 "/m" 스위치를 추가하십시오.
C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140\Platforms\x64\PlatformToolsets\v140\Toolset.targets(36,5): error
 MSB8036: The Windows SDK version 8.1 was not found. Install the required version of Windows SDK or change the SDK vers
ion in the project property pages or by right-clicking the solution and selecting "Retarget solution". [C:\dev\nodejs\n
ode_modules\java\build\nodejavabridge_bindings.vcxproj]









#### The Windows SDK version 8.1 설치 후 ####
C:\dev\nodejs\node_modules\java>if not defined npm_config_node_gyp (node "C:\dev\nodejs\node_modules\npm\bin\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "" rebuild )
이 솔루션의 프로젝트를 한 번에 하나씩 빌드합니다. 병렬 빌드를 사용하려면 "/m" 스위치를 추가하십시오.
  TRACKER : 오류 TRK0005: "CL.exe"을(를) 찾지 못했습니다. 지정된 파일을 찾을 수 없습니다.


C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V140\Microsoft.CppCommon.targets(356,5): error MSB6006: "CL.exe"이(가)
종료되었습니다(코드: 5). [C:\dev\nodejs\node_modules\java\build\nodejavabridge_bindings.vcxproj]



#### Visual Studio 재 설치 ####
(중요!!!!) VC++ 개발 도구 설치해야 함.
VS2015 설치 시 다음, 다음만 하지 말자
C:\dev\nodejs>npm install java
-
> java@0.7.2 install C:\dev\nodejs\node_modules\java
> node-gyp rebuild


C:\dev\nodejs\node_modules\java>if not defined npm_config_node_gyp (node "C:\dev\nodejs\node_modules\npm\bin\node-gyp-bin\\..\..\node_modules\node-gyp\bin\node-gyp.js" rebuild )  else (node "" rebuild )
이 솔루션의 프로젝트를 한 번에 하나씩 빌드합니다. 병렬 빌드를 사용하려면 "/m" 스위치를 추가하십시오.
  java.cpp
  javaObject.cpp
  javaScope.cpp
  methodCallBaton.cpp
  nodeJavaBridge.cpp
  utils.cpp
..\src\utils.cpp(499): warning C4244: '=': 'jchar'에서 'char'(으)로 변환하면서 데이터가 손실될 수 있습니다. [C:\dev\nodejs\node_modules\java
\build\nodejavabridge_bindings.vcxproj]
..\src\utils.cpp(616): warning C4244: '=': 'jchar'에서 'char'(으)로 변환하면서 데이터가 손실될 수 있습니다. [C:\dev\nodejs\node_modules\java
\build\nodejavabridge_bindings.vcxproj]
c:\dev\nodejs\node_modules\java\node_modules\nan\nan_new.h(214): warning C4267: '인수': 'size_t'에서 'int'(으)로 변환하 면서 데이터가 손
실될 수 있습니다. (소스 파일 컴파일 중 ..\src\utils.cpp) [C:\dev\nodejs\node_modules\java\build\nodejavabridge_bindings.vcxproj]
  ..\src\utils.cpp(685): note: 컴파일 중인 함수 템플릿 인스턴스화 'v8::MaybeLocal<v8::String> Nan::New<v8::String,const _Elem*,unsigne
  d __int64>(A0,A1)'에 대한 참조를 확인하십시오.
          with
          [
              _Elem=char,
              A0=const char *,
              A1=unsigned __int64
          ]
  win_delay_load_hook.c
     C:\dev\nodejs\node_modules\java\build\Release\nodejavabridge_bindings.lib 라이브러리 및 C:\dev\nodejs\node_modules\java\
  build\Release\nodejavabridge_bindings.exp 개체를 생성하고 있습니다.
  코드를 생성하고 있습니다.
  코드를 생성했습니다.
  nodejavabridge_bindings.vcxproj -> C:\dev\nodejs\node_modules\java\build\Release\\nodejavabridge_bindings.node

> java@0.7.2 postinstall C:\dev\nodejs\node_modules\java
> node postInstall.js

java@0.7.2 node_modules\java
├── async@1.5.2
├── find-java-home@0.1.2 (which@1.0.9)
├── nan@2.3.2
├── glob@7.0.3 (path-is-absolute@1.0.0, inherits@2.0.1, once@1.3.3, inflight@1.0.5, minimatch@3.0.2)
└── lodash@4.11.1




참고 레퍼런스
[electron 공식 quick start](http://electron.atom.io/docs/tutorial/quick-start/)
[node-java](https://github.com/joeferner/node-java)
[Cross Platform Application 개발하기 – 2편 : Electron & Node-Java](http://brantiffy.axisj.com/archives/397)

사전 처리
1. node 설치되어 있어야 함 (v4.4.5 w. npm v2.15.5)
2. python 설치되어 있어야 함 (v2.7.11 required not v3)
3. VC++ 관련 SDK 설치되어 있어야 함 (VS2015 Community Edition)
4. nw-gyp가 global로 설치되어 있어야 함

전체 과정은 아래와 같음
1. [electron 공식 quick start]에 따라 소스 작성
    - electron-prebuilt는 로컬에 설치해야 하므로 프로젝트 root에서 수행
    - node-module 폴더 생성 및 하위 폴더 생성 확인
2. 실행 확인
3. [node-java]에 따라 java 설치
    - npm은 글로벌과 로컬 설치가 있음
    - npm install java는 반드시 프로젝트 root에서 수행해야 함
    - node-module 폴더 하위에 java 폴더 생성 여부 확인
4. electron rebuild 설치
5. electron rebuild 실행 --> 별도 메시지없고 rebuild되는데 시간 많이 소요됨. 기다릴 것.
6. app 실행

배포하기
1. 전역으로 electron-package 설치
    - npm install electron-packager -g
2. 패키징 명령
    - 패키징 시 node_modules에는 java만 있으면 됨. packager에서 자동으로 빼주지 않으므로 수동 설정 필요함.
    - electron-packager . electron-test2 --platform=win32 --arch=x64 --version=1.2.3 --ignore=input --ignore=output --ignore=java_libs --asar
3. electron-test2-win32-x64 폴더 생성되고 하위에 배포 프로그램 위치함
    - 문제 : 기존 app이 resources/app으로 이동되면서 java classpath push 시 경로 문제 발생함
    - 상대 경로로 잡아도 electron-test2.exe를 기준으로 상대 경로 실행됨
