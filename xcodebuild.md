# xcodebuild.md  
___ 

## Xcode를 커맨드로 빌드할때 필요한 명령어들  
정적라이브러리등을 빌드하여 사용해야 할 경우가 종종 발생한다.   
아래와 같은 커맨드를 사용하면 굳이 Xcode어플리케이션을 사용하지 않고도 빌드가 가능하므로 편리하다.


### 시뮬레이터용 빌드하기   
XCode6부터는 약간 명령어 옵션이 바뀐듯 하다.    
XCode를 열어 Devices에서 등록되어 있는 시뮬레이터를 메모해 둔다음 명령어에 지정해 줘야 한다.    

```
xcodebuild -project [경로]/[프로젝트파일명] -scheme [타겟이름] -sdk iphonesimulator -destination 'platform=iOS Simulator,OS=9.3,name=iPhone 6s' -configuration $1 build
```

### 디아이스용 빌드하기   

```
xcodebuild -project [경로]/[프로젝트파일명] -target [타겟이름] -sdk iphoneos -configuration $1 build
```

### xcodebuild 버전확인하기   
만약 자신의 맥에 여러개의 XCode버전이 설치되어 있다면 아래의 명령어로 확인할 수 있다.

```
xcodebuild -version
```
 
### xcodebuild 버전변경하기
다른버전으로 빌드하고 싶을땐 아래의 명령어로 변경해 준다.
Xcode.app를 현재 Application에 설치되어 있는 Xcode를 지정해준다.

```
sudo xcode-select -switch /Applications/Xcode.app
or
sudo xcode-select -switch /Applications/Xcode7_3_1.app
```

### 덤으로 설치중인 sdk확인하기

```
xcodebuild -showsdks
```

### 스크립트화 해서 사용하기
빌드할 것들이 많다면 스크립트화해서 사용하자.   
예)   
kjcode/common 경로에 있는 example프로젝트를 빌드한다고 할때, 아래와 같은 스크립트로 빌드하면 편리하다.

**kjcode_build_script.sh**

```

#!/bin/sh

if [ $# -ne 1 ] ; then
	echo "please input word 'Debug' or 'Release'" 1>&2
	exit 1
fi



#build
# simulator  Regist simulator Devices use. edit simulator name
xcodebuild -project kjcode/common/example.xcodeproj -scheme example -sdk iphonesimulator -destination 'platform=iOS Simulator,OS=9.3,name=iPhone 6s' -configuration $1 build

# Device 
xcodebuild -project kjcode/common/example.xcodeproj -target example -sdk iphoneos -configuration $1 build

```

---

