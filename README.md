NODE : Q TO exit

Normal : con trỏ HEAD chỉ trỏ đến branch ,branch trỏ đến commit 

Dangerous : nếu HEAD trỏ đến commit thì nó sẽ về trạng thái "detached HEAD"

git branch (coi tất cả các branch trên local)

git branch -a (coi tất cả các branch trên local + remote)

===========================     CREAT BRANCH     =============================

                 1                 2
-- git branch branchname origin branchname [ tạo branch ở local từ một 
branch ở remote origin ( tạo 1 từ 2 )  ]

-- git checkout branchname [ checkout đến branch branchname (nếu chưa tồn tại
 sẽ lỗi ) ]

** nếu đã được ánh sạ đến một remote ( remote add đến một origin ) thì khi 
dùng --git checkout branchname-- nếu tồn tại một branch branchname trên remote 
origin thì local sẽ tạo ra một branch từ branch branchname trên remote 
[ hay bằng với  --git branch branchname origin branchname-- ]


===========================     CHECKOUT       =============================

-- git checkout branchname

-- git checkout -b branchname [ tạo branch mới từ branch hiện tại và checkout
đến  nó ]
 
                       1          2
-- git checkout -b branchname branchname [ tạo mới  branch 1 từ  branch 2  
và checkout đến nó ]

===========================     PUSH       =============================

                     1       2
--  git push origin master:master [ push từ branch master(1) trên local 
lên master(2)trên remote , nếu chưa có branch master trên remote sẽ tự
tạo ra ]

--  git push origin branchname [ push từ branch branchname trên local lên
branch có tên y hệt trên remote nếu chưa có sẽ tự tạo ](recommend)
                 
** cả hai cách trên đều có thể push 1 branch (tất cả các commit) hay có 
push những commit mới nhất < nếu được set-up-stream >

** cả hai lệnh đều không set-up-stream cho 2 branch ở local và remote mà 
chỉ push lên thôi

-- git push [ push branch hiện tại checkout tới branch mà đang được 
trancking hay set-up-stream ở trên remote origin ]

** làm sao để biết đã tracking hay set-up-stream chưa: sử dụng 
lệnh -- git remote show origin -- [ ở trong 'git pull' ]

-- git push origin HEAD:branchname [ push từ branch hiện tại lên branch 
branchname trên remote nếu chưa có sẽ tự tạo ra ] 


-- git push -u origin branchname
-- git push --set-upstream origin branchname

** cả hai lệnh là tương đương có nhiệm vụ push và set-upstream cho 2 branch 
ở local và remote

-- git push -f [--force] [ghi đề toàn bộ remote bằng local] 
** Rất nguy hiểm

-- git push ---force-with-lease [Kiểm tra remote và local xem có sự thay đổi nào trên nhánh hiện tại không [người push lên trước đó]]
** Khuyên dùng 

--
===========================     MERGE       =============================

-- git merge branchname [merge từ branch branhname đến branch mà đang được 
checkout đến hiện tại (nếu được fast-forward ) không bị conflic sẽ tự tạo
một commit merge ]

** nếu có conflict (ở cùng một dòng code 2 nội dung khác nhau) sẽ merge tất
cả những nội dung không confic còn nội dung bị conflic sẽ phải chọn 1 trong 
2 nội dung và add - commit lại 
** CHÚ Ý https://www.youtube.com/watch?v=7bPUeBQf2R4&list=PLEpE0nqWW7DLjWbGkS_B4tQOVlMDqOlOD&index=3
phút " 43:14 " 

===========================     REBASE       =============================

** giống merge khác khi merge sẽ tạo ra một commit merge còn rebase thì không
** nếu có conflic thì -- git rebase --continue

-- git rebase branchname [ đưa các commit cửa branch đang checkout hiện tại
lên top cửa branch branchname khác vs merge sẽ lưu các commit theo thời gian 
tạo của nó ]

===========================     DELETE       =============================


-- git branch -d branchname [ xóa branch branchname  ]

** không thể xóa branch branchname khi đang checkout ở nó phải checkout 
qua branch khác

===========================     FETCH       =============================
 
-- git fetch origin [ (fetch : lấy) lấy toàn bộ từ origin về local ]

-- git fetch origin branchname [ lấy toàn bộ dữ liệu từ branch branchname
trên remote về ]

 ** 2 câu lệch trên chỉ fetch từ remote origin branch về local origin branch

===========================     PULL      =============================

-- git pull [ git fetch + git merge ]

-- git pull origin branchname [pull từ branch branchname về nhánh hiện tại]

-- git pull --rebase [ git fetch + git rebase ]

===========================     STASH      =============================

-- git stash [ lưu trữ tạm các file đã add. (ở trạng thái stage) mà không 
cần commit ]

-- git stash list [ show các stash đã lưu ]

-- git stash pop stash@{ number_of_stash } [ lấy file đã lưu chữ ra ]
===========================    STASH     ==============================
-- git stash save [message] [ lưu công việc hiện tại vào 1 stash]

-- git stash list [-p] [ xem list stash đang có -p: xêm thêm cả nội dung]

-- git stash show stash@{x} [xem nội dung của stash x]

-- git stash apply stash@{x} [lấy stash x ra]

-- git stash pop stash@{x} [lấy stash x ra và remove nó khỏi list stash]

-- git stash drop stash@{x} [xóa stash x]

-- git stash clean [xóa toàn bộ stash] 
===========================     RESET       =============================


** git reset có 3 loại (option)
				  Commit    | Changed_in_Staging_area    |  Changed_in_working_directory
	--------------------------------------------------------------------------------------------
	+ --hard		    x			x				x
	--------------------------------------------------------------------------------------------
	+ --mixed(default)	    x			x				v
	--------------------------------------------------------------------------------------------
	+  --soft		    x			v				v
	--------------------------------------------------------------------------------------------
	
	*  git reset --{option} {hash commit | HEAD... | filename}
	
	
--git reset (name-file)[ reset tất cả các file hoặc file name-file stage 
về unstage bằng với --git restore --unstage filename-- ]

-- git reset HEAD~1 [ reset 1 commit , đưa head lui 1 commit và giữ nguyên
các thay đổi  ]

** có thể sử dụng các số khác thay cho số 1  nhưng khi đã ở commit đầu tiên 
thì không thể reset, đưa tất cả các file về trạng thái unstage
** đưa tất cả các file về trạng thái stage
** nguy hiểm ít nên dùng
** sử dụng " HEAD^ " commit hiện tại
** tất cả các câu lệnh trên đều không thể reset initial commit (first commit)
 có thể sử dụng -- git update-ref -d HEAD --
** để cập nhập thay đổi này trên remote sử dụng -- git push --force origin--

===========================     CLEAN       =============================

-- git clean -n [xem tất cả các file, folder sẽ được xóa]

-- git clean **option** [xóa các file và folder untrack]
	+ -f (file): xóa file
	+ -d (folder): xóa folfder
	+ -x :ignore file
	
===========================     DELETE BRANCH       =============================

-- git branch -d localBranchName [delete branch locally]

-- git push origin --delete remoteBranchName [delete branch remotely]

===========================     WORKTREE       =============================

===========================     CHERRY-PICK       =============================

** cherry-pick sử dụng để lấy 1 commit bất kì từ 1 branch khác đến branch hiện tại

-- git cherry-pick {option} commit-hash [lấy commit và tạo lại 1 commit rồi add vào branch hiện tại]

** option
	+ --no-commit  [chỉ lấy các thay đổi chứ ko commit . Có thể commit sau đó]
	
	
===========================     REFLOG       =============================

** show ra những thứ đã làm ở local-repo

-- git reflog [ HEAD@{number} ]

-- git reflog show {branch-name}

===========================     REBASE INTERACTIVE       =============================

-- reword [viết lại tên commit]

-- delete [delete commit]

-- reordering [thay đổi thứ tự commit]

-- squashing [  ghép nhiểu commit lại thành một ]

-- spliting [ chia commit ]


=========================     MORE UTIL       =============================

-- touch filename.abc (tạo ra một file ở working directory )

-- notepad filename.abc ( mở file bằng nodepad  )

-- git remote show origin ( show ra info của remote origin  )

-- git remote -v ( show re các remote được ánh xạ )

-- git log --oneline --decorate --graph (--all) [ show tất cả các branch và
commit theo graph ] 

-- git commit --amend -m "New commit message." [thay đổi tên commit mới nhất]

-- git commit --amend (--no-edit) [ không tạo commit mới đưa các file ở stage
vào commit hiện tại có thể thay đổi massage ]

-- git diff commithasd [ so sánh commit hiện tại  với commit có commithash ]

-- git remote set-url origin newurl [ đổi url mà git ánh xạ đến ]

-- git remote rm <remote-name> [xóa ánh xạ đến remote]

-- git diff [file name] [show change trong file]

-- git commit --amend --no-edit [ commit changed to previous commit , not create new commit ]

-- git fetch remote-name pull/id-PR/head:branch-name-on-local [ fetch from pull request ]



