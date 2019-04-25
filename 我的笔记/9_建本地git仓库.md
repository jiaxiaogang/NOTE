| 步骤 | TITLE | COMMAND | DESC |
| --- | --- | --- | --- |
| 1 | 定位到共同库地址 | cd /Volumes/Public/推荐端/soft/ |  |
| 2 | init一个库 | git --bare init | `//之所以不用git init是因为一push就报错说git reset --hard什么的` |
| 3 | 定位到私有库父目录 | cd /Volumes/APPLE\ HDD/ | 如果本地有冲突,可以先用个别名,如soft2 |
| 4 | clone项目 | git clone /Volumes/Public/推荐端/soft/ |  |
| 5 | 定位到私有库地址 | cd /Volumes/APPLE\ HDD/soft |  |
| 6 | 提点文件试试 | touch readme.md |  |
| 7 | add一下 | git add . |  |
| 8 | commit下 | git commit -m "readme.md" |  |
| 9 | push下 | git push |  |
| 10 | 成功 |  | 此时打出[new branch] master -> master什么的; |
