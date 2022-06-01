git 연습용 repository



case1.
-상황 : 브랜치 여러개 생성 - unrelated history branch 생성(추측) - pull request 버튼은 뜨지만 merge할게 없다고 나옴
-예방방법 : 일단 pull로 당겨서 commit history를 같게 맞춰줘야한다
-해결방법 :  연관없는 브랜치를 병합하려고하면 일단 There isn't anything to compare이 뜰거다
merge할수도 없을거고



case2.
-상황 : 
git repository에 있는 모든 내용을 제거하기위해 local repository에서 remote repository에 있는 최신 commit 내용을 pull 해줬다
하지만 이 remote repository가 가진 branch들의 최신 commit 내용이 모두 달랐다 
팀원1이 remote repository에 있는 최신내용을 가져가서 branch1을 생성하고 commit1을 해주고 remote repository에 push 해줬다
팀원2가 remote repository에 있는 최신내용을 가져가서 branch2를 생성하고 commit2를 해주고 remote repository에 push 해줬다
팀원3이 remote repository에 있는 최신내용을 가져가서 branch3을 생성하고 commit3를 해주고 remote repository에 push 해줬다
팀원4가 remote repository에 있는 최신내용을 가져가서 branch4를 생성하고 commit4를 해주고 remote repository에 push 해줬다

-해결방법 : (추측) remote repository에 있는 branch들과 이름이 같게 브랜치를 생성하고 모든 브랜치를 ... 음 좀 더 생각해봐야겠다 (의문1. 이름이 같다고 remote repository의 branchname1이 local repository에 생성된 branchname과 같다고 할수있나? 이름만 같은거고 고유아이디값같은게 다른거 아닌가?) -> 당연히 안된다 따로 인식을 시켜줘야했음 (remote update)


case3.
-상황 : 
1.git clone으로 git init 없이 local repository 지정 후 
2.git add . 입력
3. 
warning: LF will be replaced by CRLF in demo/.gitignore.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/.mvn/wrapper/maven-wrapper.properties.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/mvnw.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/mvnw.cmd.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/pom.xml.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/src/main/java/dev/sample/demo/DemoApplication.java.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/src/main/resources/application.properties.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in demo/src/test/java/dev/sample/demo/DemoApplicationTests.java.
The file will have its original line endings in your working directory
경고문 출력

모르는것 : HEAD는 어디에?

해결방법 : 그냥 단순 경고 메세지임
리눅스에서 줄바꿈(개행)은 End of Line을 Line Feed(LF)로 나타내고
윈도우에서 줄바꿈(개행)은 Carriage Return (CR) + Line Feed(LF)로 나타내기때문
CRLF에서 LF로 변환해서 처리할것이라는 경고성 메세지임

case4.
-상황 : A 프로젝트에서 기존의 A브랜치 외에 B브랜치,C브랜치를 생성했다. (이때 모든 브랜치의 history는 같다)
 그런데 아무 변경사항도 없어야 할 B브랜치에 실수로 BB라는 파일이 추가됐다
 BB를 commit 하지않고 B를 변경전으로 유지하는방법은?
 
 단, BB를 삭제하는건 안된다(삭제하면 delete:BB 이런식으로 뜨지않을까?)
 
 
-시도 : git pull origin B브랜치 했지만 실패했다

From https://github.com/remoterepositoryaddress
 * branch            B브랜치     -> FETCH_HEAD
Already up to date.


-해결방법: git clone을 쓰면 해결될것 같긴하다(안해봄)





토큰관련 
-해결방법1 : 토큰써야할때 비밀번호를 쓴거니 토큰을 적는다
-해결방법2 : 토큰을 입력해야하는것도 안나오는 경우 계속 그 repository만 쓸 경우 자격 증명 관리자에 들어가서 비밀번호를 그 repository 관리자의 토큰으로 변경해준다 그냥 로그인창을 띄우고싶다면 그냥 자격 증명 관리자에서 깃허브 아이디랑 비밀번호가 자동입력 되어있는걸 삭제해준다 끝


