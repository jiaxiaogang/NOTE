```c
1. 换brew腾讯源
  a. 替换brew.git:
  cd "$(brew --repo)"
  git remote set-url origin https://mirrors.cloud.tencent.com/homebrew/brew.git

  b. 替换homebrew-core.git:
  cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
  git remote set-url origin https://mirrors.cloud.tencent.com/homebrew/homebrew-core.git

  c. 更新bottles源:
  echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.cloud.tencent.com/homebrew-bottles' >> ~/.bash_profile
  source ~/.bash_profile

2. 安装basicTex (大约300MB)
brew cask install basictex

3. 更新tlmgr
sudo tlmgr update —self

4. 在atom用latex进行build,如果报latexmk not found
sudo tlmgr install latexmk

5. 在atom用latex进行build,如果报ctex.sty not found
sudo tlmgr install gen-misc//报错,再试以下命令;
sudo tlmgr install ctex//后解决;

6. 在atom用latex进行build,如果报multirow.sty not found;
sudo tlmgr install multirow

7. 最终还是报三个错:
   * latexmk: Failure in some part of making files.
   * Package ctex: Support package `expl3` too old
   * Critical Package ctex: CTeX fontset `mac` is unavailable in current

8. 至此,放弃挣扎,下次玩的时候,直接安装完全版吧;
  * 用uninstall一一删除以上安装;
  * 完整版占用空间大概6G;
```
