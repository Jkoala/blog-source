##  git删除远程仓库上已提交的文件/文件夹
https://blog.csdn.net/niwenroudelian/article/details/127878497

1.  预览将要删除的文件（如果不清楚该目录下是否存在不应该删除的文件）
git rm -r -n --cached 文件/文件夹名称

2.  确定无误后删除文件（不会删除本地的文件或文件夹）
git rm -r --cached 文件/文件夹名称

3. 提交到本地并推送到远程服务器