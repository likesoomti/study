# git 기본 명령어 쉽게 이해해보기

소스트리를 이용한 깃헙 프로젝트 생성하기를 만들다가, 이에 대한 개념 설명이 필요할 것 같아서 정리를 해봅니다.

## 깃에 대한 간단한 설명

제가 쉽게 이해한 깃은

### 내 컴퓨터에있는 파일들을 인터넷에 쉽게 올리기 위한 수단 

입니다. 

보통 우리가 조별과제할때 수정사항이생기면 계속 파일을 `최종.hwp` `진짜최종.hwp` `최종진짜진짜.hwp` `최종진짜이게진짜.hwp` 이런식으로 여러 파일들을 복제해서 보내는 경험이 다들 있으실 거에요. 그럼 같은 파일인데 나중에 뭐가 진짠지도 헷갈리고... 컴퓨터도 드러워지는 불상사가 발생합니다. 

깃을 사용하면 여러 파일을 안남기고, 하나의 파일을 인터넷에 공유하고 같이 기록을 남겨 편리하게 해결할 수 있습니다.

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add12.png?raw=true)

위 사진처럼 제가 폴더에 내용을 추가하거나, 변경된 기록을 남겨주는데요 이것을 **커밋** 이라고합니다.

이 커밋들이 쌓여서, 어느 시점에 모든 기록이 끝나면 **푸시** 를 하게되고, 푸시를 하면 제 깃주소 안에  저장되게 됩니다!

이부분을 헷갈려 하시는 분들이있는데요. 여러 명령어들과 함께 택배로 이해해 봅시다



### 택배로 비유해서 이해해보자

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add23.png?raw=true)

내 컴퓨터에서 프로젝트를 올리는게 아니라, 내 깃 주소에서 프로젝트를 만드는 경우 보여주는 명령어입니다. 

이에 대한 개념을 알고있어야지 커밋과 푸시를 제대로 이해할 수 있습니다.

그걸 예전에 ppt 로 간단히 택배에 비유하여 설명을 했던걸 붙혀 놓아 설명하면서 쉽게 설명을 해보겠습니다.



### 깃 초기 설정하기



#### git init

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add13.png?raw=true)

`init` 은 `initialize` 의 약자로 새로 만들겠다! 라는 뜻입니다.

따라서 `git init` 이라는 것은. 해당 프로젝트(=폴더)를 git 으로 만들어줘! 라고 명렁해 주는거에요. 

내컴퓨터와 깃헙 url 을 연결할때는. `git` 을 통해 연결되기 때문에 이 명령어를 써야합니다!

##### 주의 : github 과 git 은 달라요!

`github` 은 `git` 를 관리해주는 저장소에요. `git` 은 파일의 로그 , 버전? 을 관리하게 만들어주는 친구입니다.

너무 어려우면

**내 컴퓨터** 에 있는 프로젝트(=폴더)  **github** 에 택배처럼 보내야하는데, **git**이라는 **상자**를 통해 보내준다! 라고 생각하시면 더 쉬울까요..?



#### git add 

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add14.png?raw=true)

git add 는 제가 **github**에 보낼 파일들을 상자에 넣는 역할입니다 `.` 을 쓰면 모든 파일을 넣어주는데요,

보통 프로젝트를 협업할시에는 내 컴퓨터에 사양과 친구의 사양이 달라 보내지 말아야할 파일들이 몇개 있습니다. 그게 없다면 그냥 쉽게 `.` 을 통해 다 넣어주시면 됩니다.

택배로 설명하면, 저는 **내컴퓨터에** 서 **깃헙** 에 보낼 파일들을 상자에 부랴부랴 쌓은거에요



#### git commit

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add15.png?raw=true)

`git commit` 은 테이프 칠을 한 것이라고 생각하면됩니다.

보통 `git commit -m '깃헙 내용을 쉽게 정리해봤다'` 이런식으로 뒤에 `-m` 을 붙혀서 메세지를 남기는데요 

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add16.png?raw=true)

보통 우리가 조별과제할때 저런식으로 파일이 복제되는데, 

저렇게 제목만 복제되는게 아니라 저 맨 위에 나왔던 사진처럼  메세지로 남아서 기록되게 됩니다.

저는 **내컴퓨터에** 서 **깃헙** 에 보낼 파일들에 "최종 프로젝트 라이더 친구들 이름 제거^^" 라고 기록을 남겨주는 거에요.

조별과제에 있으면 콜라보해서 얼마나 했는지 교수님이 알아줬으면 좋겠네요.. 깃 상용화 소취 



#### git remote add origitn git url 주소

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add17.png?raw=true)



간단하게 설명하면, 이제 제 컴퓨터에서 깃헙 프로젝트에 

저는 **내컴퓨터에** 서 **깃헙** 에 택배를 보낼때는 어디로 보낼지 주소가 필요하겠죠? 프로젝트는 고유의 주소를 갖고있는데 그 주소를 적어주는 겁니다. 이렇게하면  **내컴퓨터에** 의 폴더랑 **깃헙**  이 연결이 됩니다!

#### git push

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add18.png?raw=true)

**내컴퓨터에** 에서 보낸 파일을 **깃헙** 에 택배를 보내듯이 전송! 합니다. 그럼 github 주소를 들어가보면 올라온 것을 볼 수 있습니다.



처음 연결을 할 때만 `init`과  `remote orgin` 을 사용하기때문에, 이후에는 이 부분 없이

`add`

`commit -m `

`push` 를 사용하면 됩니다.



### 깃 내용 추가 및 수정 하기

##### 

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add19.png?raw=true)



![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add20.png?raw=true)

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add21.png?raw=true)

![Alt text](https://github.com/likesoomti/STUDY/blob/master/GITHUB%20/img/add22.png?raw=true)