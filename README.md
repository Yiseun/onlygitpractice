git 연습용 repository



case1.
-상황 : 브랜치 여러개 생성 - 다른 commit history 생성(추측) - pull request 버튼은 뜨지만 merge할게 없다고 나옴
-해결방법 : 일단 pull로 당겨서 commit history를 같게 맞춰줘야한다

case2.
-상황 : 
git repository에 있는 모든 내용을 제거하기위해 local repository에서 remote repository에 있는 최신 commit 내용을 pull 해줬다
하지만 이 remote repository가 가진 branch들의 최신 commit 내용이 모두 달랐다 
팀원1이 remote repository에 있는 최신내용을 가져가서 branch1을 생성하고 commit1을 해주고 remote repository에 push 해줬다
팀원2가 remote repository에 있는 최신내용을 가져가서 branch2를 생성하고 commit2를 해주고 remote repository에 push 해줬다
팀원3이 remote repository에 있는 최신내용을 가져가서 branch3을 생성하고 commit3를 해주고 remote repository에 push 해줬다
팀원4가 remote repository에 있는 최신내용을 가져가서 branch4를 생성하고 commit4를 해주고 remote repository에 push 해줬다

-해결방법 : (추측) remote repository에 있는 branch들과 이름이 같게 브랜치를 생성하고 모든 브랜치를 ... 음 좀 더 생각해봐야겠다 (의문1. 이름이 같다고 remote repository의 branchname1이 local repository에 생성된 branchname과 같다고 할수있나? 이름만 같은거고 고유아이디값같은게 다른거 아닌가?)

case3.
-상황 : 연관없는 브랜치 병합

case4.
-상황 : 

토큰관련 
-해결방법1 : 토큰써야할때 비밀번호를 쓴거니 토큰을 적는다
-해결방법2 : 토큰을 입력해야하는것도 안나오는 경우 계속 그 repository만 쓸 경우 자격 증명 관리자에 들어가서 비밀번호를 그 repository 관리자의 토큰으로 변경해준다 그냥 로그인창을 띄우고싶다면 그냥 자격 증명 관리자에서 깃허브 아이디랑 비밀번호가 자동입력 되어있는걸 삭제해준다 끝


