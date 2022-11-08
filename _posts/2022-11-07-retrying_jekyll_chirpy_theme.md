---
title:  "다시 시도하는 Chirpy 테마"  
date:   2022-11-07 23:14:09 +0900
categories: [Github-Pages, jekyll blog]
tag: [jekyll, blog, chirpy-theme,EXIT CODE1, EXIT CODE16, init.sh ]
toc: true
---

## Chirpy Theme 설치

### 오류의 원인

앞에서도 언급했듯이 처음에 Chirpy 테마 설치 시에 잘못된 점은  __.gitignor__ 파일에서 Gemfile.lock 항목을 지웠어야 하는데 오히려 디렉토리에 있는 Gemfile.lock 파일을 지워버리고   __.gitignor__  파일에 Gemfile.lock 항목을 또 한번 적어버린 점이다. 이렇게 하니 git push 에서 에러가 발생하는것은 당연한 것인지도 모른다.
(다른 뉴비분들이 나같은 같은 실수를 반복하지 않기를 바란다.)
안타까운 것은 로컬(localhost:4000)에서 이런 종류의 오류가 걸러지지 않는다는 것이다. ( 뒤에도 나오지만 로컬에서 걸러지지 않는 많은 에러들 때문에 리모트에서 반복되는 빌드에러가 발생한다. )

### Windows PowerShell 에서 .sh script를 실행

아무튼 잘못된 점을 인지하고 곳바로 이를 바로잡아 다시 시도하였다. 이 모든 오류의 출발점은 git bash command 창에서 `tools/init.sh`를 실행한 것이 아래에서 처럼 오류 메시지를 발생 시키고 올바른 진행이 되지않는 때문에 init를 수동으로 진행하는 과정에서 발생한 것이다.

![init.sh script error](/images/2022-11-07/unstaged_files_2022_11_07.png){:class="img-responsive"}


따라서 이번에는 여러종류의 다른 실행 창들에서  `tools/init.sh` 를 시도해보니 다행히 `windows PowerShell` 에서 오류없이 잘 진행되었다. 

![sh script on PowerShell](/images/2022-11-07/initilize-2022-11-04%20135258.png){:class="img-responsive"}

`` bash`` 명령을 인식하지 못해서 이를 제거하고 입력했더니 잠시동안 작은 창하나가 생겨난 후에 사라졌다.
_posts 디렉토리에 모든 md 파일들이 지워져있는 것을 보니 명령이 잘 실행된 것이라고 생각되었다. 
    
    
### 걸러지지 않는 ERROR1 (EXIT CODE16)

무사히 잘 진행되는가 싶었지만 build과정에서 또 다시 에러가 발생하는데 


![page-deploy.yml build error](/images/2022-11-07/error%20code16%20-%202022-11-04%20143534.png){:class="img-responsive"}


이번에는 에러를 잘 추적하여 에러 문구를 구글링하고 해결방법을 찾았다.


``` Ruby
 bundle lock --add-platform x86_64-linux 
```

이걸 명령 창에서 실행하고 __github desktop__ 을 살펴 보니 `Gemfile.lock` 파일이 몇 군데 변경된 것을 알 수 있었다. 이걸 다시 push하니 이번엔 build 과정이 에러없이 잘 진행되었다.
(사람들은 github GUI 프로그램으로 __github desktop__ 보다는 __sourcetree__ 를 추천하지만 나같은 뉴비들에게는 이런 부분을 알 수 있게 해준다는 점에서 __github desktop__ 이 유용성이 아주 없는 것도 아닌 것 같다. 나중에 빌드 에러도 아니면서 사이트 접속이 않되는 상황을 마주했는데  이 파일을 원상복귀하고 다시 ``bundle lock --add-platform x86_64-linux`` 명령을 입력하는 방법으로 해결했기 때문이다. )  
  

![Update Gemfile.lock](/images/2022-11-07/Gemfile.lock%20update%202022-11-07%20230743.png){:class="img-responsive"}

(  버전 5.0 이전 버전 의 README.MD 파일을 살펴보면 위 명령은 linux 가 아닌 시스템인 경우에 필요한 내용이라고 하는데 5.0 이상 버전 배포 과정에서 실수로 삭제된 것 같다. )

### 걸러지지 않는 ERROR2 (EXIT CODE1)

이번 에러는 post글 첨부파일 이미지나 favicon같은 것들로 부터 발생했다.
  
  
![internal image does not exist](/images/2022-11-07/error-code1-2022-11-04%20143703.png){:class="img-responsive"}
테마 변경 과정에서 실수로 첨부파일 이미지를 디렉토리에 넣지않았다.

![favicon file name miss match](/images/2022-11-07/error-code1-2022-11-04%20232641.png){:class="img-responsive"}


테마의 설명파일에 소개된 대로 favicon을 제작해 설치했으나 파일명이 다른 이미지가 있었다.

