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



case5. main branch 내용 무결성유지, 다양한 브랜치 활용


폴더만들고 cd 경로
git clone할 경로 만들어주기
cd 안쪽으로 경로이동
이 시점에서 history는 하나(클론한 repository) (깃 클론으로하면 remote 설정해줄필요없음)
수정할 브랜치 생성 (branch1)
여기서 브랜치는 둘이됐지만 같은 history를 가지고있음 
create 
update
delete
localmain
(난 
155modi
  455modi
  515665modi
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
이렇게 했다 remotes/origin/HEAD는 origin으로 향하는 HEAD인것같은데 정확하게는 모르겠다)

하지만 같은파일을 수정해서 반드시 충돌이 일어날것
git checkout branch1,2,3,4로 일단 push해서 remote repository branch에 local repository branch를 연동시켜줌
git push --set-upstream origin branch1
git push --set-upstream origin branch2 다른브랜치에서도 할수있나? 되네
git push --set-upstream origin branch3
git push --set-upstream origin branch4
다 연동됐음 (아직까지는 초기 history를 가지는 4개의 브랜치)
목표는 branch4에 다 합치고 main에 합치는것

git checkout branch1 
수정하고
이제 얘는 다른 history를 가진다 
(git checkout branch2를 하면 branch1에서 수정된 파일이 수정안되어있어야하는데 수정되어있다 왜이러지? - 근데 협업시에는 일단 문제가 없을것으로 보이긴하다 일단 git checkout branch2,3,4에서는 원래 초기 history를 가진 remote repository에서 다시 pull해준다 (원래대로 돌아가서 branch1과 branch2,3,4랑 데이터가 다를것이라 예상함) 
그대로 branch1에서 변경된점이 branch2,3,4에도 반영되어있고
git pull origin branch2를 해도 git branch2가 이전내용으로 업데이트 안된다 add를 하고 다시 한번 체크해봐야겠다 
branch1에서 add했다 다른 브랜치에도 add 되어있는지 확인 branch2,3,4에도 add되어있음)
지금 branch1에서 파일을 수정해서 커밋으로 올렸다(아마 HEAD)
(이 상태에서 git pull origin branch2,3,4를 한다면 branch1과 다른 브랜치 3개를 만들수있을것이라 예상함)
수정내용이 아직 staged area '이하'에 있을때는 모든 브랜치에서 확인할수있지만
commit되는순간 이젠 그 커밋을 올린 브랜치에서 밖에 확인을 할수없는것같다 
git pull origin branch2,3,4를 안했는데도 branch1과 다른 브랜치 3개가 만들어졌다
이제 브랜치의 상태는 이렇다
remote repository : A
branch1 : A#
branch2 : A
branch3 : A
branch4 : A
최종목표는 branch4를 최신커밋들을 다 병합한걸로 만들고 remote repository랑 병합하는것
여기서 이제 branch2를 A$로 만들어서 병합해볼예정이다

난 여태까지 기준을 branch로 생각하고 병합같은걸 생각하니 현황파악을 잘 못했던것같다
기준을 commit log로 생각하고 병합해야하는것같다

git checkout branch4 로 해주고
git log 로 branch1에서 commit한 내용을 병합해줬다
git merge commit
git commit 내용이 branch1에서만 확인된다 branch4에서는 병합할수없음
git merge branch1을 사용하기로한다
git log로 확인해주니 branch1의 commit log가 성공적으로 병합됐다 아직 코딩을 잘하는게 아니라 이렇게 생각대로 문제없이 되는게 너무 좋다
remote repository : A
branch1 : A#
branch2 : A
branch3 : A
branch4 : A#
이제 branch4를 push하고 branch2를 pull하지않고 변경해볼예정이다
아마 충돌이 일어날것이다
remote repository와 branch2 commit history가 다르니깐
일단 계획은 cherrypick으로 branch1의 commit을 branch로 가져온다
예상은 A$# 이런식으로 되서 안될것같은데
A#$로 시간순서대로 되는건가?
일단 아무리 연습이라도 원하는대로 됐으면해서 좀 더 찾아봐야겠다
좀 찾아봤고
일단 branch1변동사항을 branch4로 합쳐서 branch4로 push하는건 됐다
remote repository에서 현황을보면
remote repository : A#
branch1 : A
branch2 : A
branch3 : A
branch4 : A#
이렇게 되어있다 branch1,2,3은 아직 아무런 push를 안했기때문
이제 branch2에서 최신커밋을 반영하지않고 다른파일을 수정한뒤 올려볼예정이다
다른파일을 고치면 merge할때 충돌이 안일어나지않을까?
:white_check_mark: Test: add related history branch

이제 commit history가 달라졌다 file은 다른파일을 수정했고
에러가 난다면 다른파일이더라도 commit history를 계속해서 반영해줘야한다는뜻이고
에러가 안난다면 다른파일이라면 commit history는 그 파일만 변경되지않으면 된다는뜻이다
후자가 아닐까?
일단 local repository와 remote repository git commit hash값을 적어보면
local repository:
branch1 : A# ad0cefe1  29c39b73b f89d290d50 937a825c7
branch2 : A$ ad0cefe1  29c39b73b f89d290d50 9f157e
branch3 : A ad0cefe1  29c39b73b f89d290d50
branch4 : A# ad0cefe1  29c39b73b f89d290d50 937a825c7

remote repository : 
branch1 : A ad0cefe1  29c39b73b f89d290d50
branch2 : A ad0cefe1  29c39b73b f89d290d50
branch3 : A ad0cefe1  29c39b73b f89d290d50
branch4 : A# ad0cefe1  29c39b73b f89d290d50 937a825c7

여기서 branch1 다른건 당연히 branch4로 모아서 push해줬기 때문이다
merge가 됐다
후자가 맞다
다른파일이면 commit history는 근본적인것만 같으면 된다 (예전 팀워크할때 실패했던이유는 ... 음... 정확히 봐야 알겠는데...)

그런데 문제가 생겼다
아까는 그냥 git push origin branch4를 하면 
remote repository의 main에 반영이 됐었는데 안됐다
이러면 안되는데

git checkout remote/origin/main해서 그냥 단순하게 병합해줌
commit 3244c086a940cf539bb5c7c47a063bb2bf668c8b (HEAD, or
Merge: 937a825 9f157e8                                   
Author: Seun Lee <sleet99@naver.com>                     
Date:   Sat Jun 4 23:41:56 2022 +0900                    
                                                         
    Merge branch '455modi' into localmain                
                                                         
commit 9f157e8ac9702d335f76ef3fc71ff391dba25e1e (455modi)
Author: Seun Lee <sleet99@naver.com>                     
Date:   Sat Jun 4 23:36:07 2022 +0900                    
                                                         
    :white_check_mark: Test: add unrelated file          
                                                         
commit 937a825c7d031ab0b263b929761efaab20dffe1d (155modi)
Author: Seun Lee <sleet99@naver.com>                     
Date:   Sat Jun 4 22:35:55 2022 +0900                    
                                                         
    :white_check_mark: Test: add related history branch  
                                                         

성공 모든게 반영됐다

근데 이게 아닌가

브랜치 정보에 HEAD detached at 3244c08 이렇게 나온다
remote/origin/main은 github의 main이 아닌것같다 

git push origin HEAD:main
을 해줬다

둘다 실패함


왜 실패했는지는 모르겠는데 github에서 gui로 병합함 왜 안된거지

 
그리고 여기서 
branch2에서 515665를 지우고
branch3에서 515665를 수정한다
- 이부분에서 conflict 생기는거 일단 둘중에하나를 add하거나 rm하는걸로 해결했긴한데- 좀 더 보완이 필요해보임




git add. commit push


155
plz si

455
(none)

515665
fdgdfgdsdfsdfsdfs
s
df
s
fs
df
sfd



case5.1 report
[515665modi 49585d8] :white_check_mark: Test : Edit 515665.txt
 1 file changed, 2 insertions(+)

C:\Users\Playdata\Desktop\G\onlygitpractice(515665modi -> origin)
λ git branch -a
  155modi
  455modi
* 515665modi
  localmain
  main
  remotes/origin/155modi
  remotes/origin/455modi
  remotes/origin/515665modi
  remotes/origin/HEAD -> origin/main
  remotes/origin/localmain
  remotes/origin/main

C:\Users\Playdata\Desktop\G\onlygitpractice(515665modi -> origin)
λ git checkout localmain
Switched to branch 'localmain'
Your branch is up to date with 'origin/localmain'.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git merge 515665modi
Merge made by the 'ort' strategy.
 515665.txt | 2 ++
 1 file changed, 2 insertions(+)

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git merge 455modi
CONFLICT (modify/delete): 515665.txt deleted in 455modi and modified in HEAD.  Version HEAD of 515665.txt left in tree.
Automatic merge failed; fix conflicts and then commit the result.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git fetch 455modi
fatal: '455modi' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git merge --continue
error: Committing is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
U       515665.txt

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push origin main
To https://github.com/Yiseun/onlygitpractice.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Yiseun/onlygitpractice.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push origin localmain
To https://github.com/Yiseun/onlygitpractice.git
 ! [rejected]        localmain -> localmain (fetch first)
error: failed to push some refs to 'https://github.com/Yiseun/onlygitpractice.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git checkout localmain
error: you need to resolve your current index first
515665.txt: needs merge

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git merge 515665.txt
error: Merging is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git add 515665.txt

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git checkout localmain
Already on 'localmain'
Your branch is ahead of 'origin/localmain' by 2 commits.
  (use "git push" to publish your local commits)

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push origin localmain
To https://github.com/Yiseun/onlygitpractice.git
 ! [rejected]        localmain -> localmain (fetch first)
error: failed to push some refs to 'https://github.com/Yiseun/onlygitpractice.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git remote -a
error: unknown switch `a'
usage: git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename [--[no-]progress] <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>

    -v, --verbose         be verbose; must be placed before a subcommand


C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git remote -v
origin  https://github.com/Yiseun/onlygitpractice.git (fetch)
origin  https://github.com/Yiseun/onlygitpractice.git (push)

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git status
On branch localmain
Your branch is ahead of 'origin/localmain' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push
To https://github.com/Yiseun/onlygitpractice.git
 ! [rejected]        localmain -> localmain (fetch first)
error: failed to push some refs to 'https://github.com/Yiseun/onlygitpractice.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git fetch origin localmain
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 3.72 KiB | 165.00 KiB/s, done.
From https://github.com/Yiseun/onlygitpractice
 * branch            localmain  -> FETCH_HEAD
   3244c08..e84c032  localmain  -> origin/localmain

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git branch localmain
fatal: a branch named 'localmain' already exists

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push origin localmain
To https://github.com/Yiseun/onlygitpractice.git
 ! [rejected]        localmain -> localmain (non-fast-forward)
error: failed to push some refs to 'https://github.com/Yiseun/onlygitpractice.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git pull origin localmain
From https://github.com/Yiseun/onlygitpractice
 * branch            localmain  -> FETCH_HEAD
Merge made by the 'ort' strategy.

C:\Users\Playdata\Desktop\G\onlygitpractice(localmain -> origin)
λ git push origin localmain
Enumerating objects: 10, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 815 bytes | 271.00 KiB/s, done.
Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/Yiseun/onlygitpractice.git
   e84c032..7220b65  localmain -> localmain




related history branch
155는 그냥 수정해서 올리고

deleted one
그다음 나머지들은 pull해서 다운받음
455는 515665를 삭제해야함

intended conflict (delete file)

515665는 수정을 하고올려야함 





토큰관련 
-해결방법1 : 토큰써야할때 비밀번호를 쓴거니 토큰을 적는다
-해결방법2 : 토큰을 입력해야하는것도 안나오는 경우 계속 그 repository만 쓸 경우 자격 증명 관리자에 들어가서 비밀번호를 그 repository 관리자의 토큰으로 변경해준다 그냥 로그인창을 띄우고싶다면 그냥 자격 증명 관리자에서 깃허브 아이디랑 비밀번호가 자동입력 되어있는걸 삭제해준다 끝


