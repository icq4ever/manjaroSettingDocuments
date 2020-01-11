# manjaroSettingDocuments
아치리눅스 만자로 배포판 정리

## 배포판 선택
-> [Manjaro XFCE Edition](https://osdn.net/dl/manjaro/manjaro-xfce-17.1.12-stable-x86_64.iso) : lightweight desktop environment(개인적으로 깔끔하다 생각)

## nvidia setting
### bumblebee
```
$ yaourt -s virtualgl #optirun으로 앱 실행시 필요
$ gpasswd -a <user> bumblebee
```

## 유용한 유틸리티
### AUR
-> [http://archlinux.fr/yaourt-en/](http://archlinux.fr/yaourt-en/)
```
$ sudo pacman -S base-devel

git clone https://aur.archlinux.org/package-query.git
cd package-query
makepkg -si
cd ..
git clone https://aur.archlinux.org/yaourt.git
cd yaourt
makepkg -si
cd ..
```
### oh-my-zsh
```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
### fast install (mine)
```
$ sudo pacman zsh vim terminator 
$ yaourt -s vscode
$ yaourt -s iosevka-term

```
### [rofi](https://github.com/DaveDavenport/rofi)
스팟라이트/alfred와 같은 간단 런처
```
$ sudo pacman -S rofi
```
- 테마 선택 : `rofi-theme-selector` 로 선택 후 `alt+a`
- keyboard shortcut command : `rofi -show drun`

### [zeal](https://github.com/zealdocs/zeal)
오프라인 도큐먼트 문서. dash for mac과 같다. \
Qt관련 버그가 있는듯. 예전엔 HiDPI 관련 이슈로 아이콘등이 이상하게 크기가 이상하더니, 아에 구동이 안되기도 한다.\

github에서 직접 소스를 받아 빌드하여 실행하고, 쉘 스크립트를 만들어 QT옵션을 주며 실행토록 한다.
```
$ git clone https://github.com/zealdocs/zeal
$ cd zeal
$ mk build && cd build
$ cmake ..
$ make && sudo make install

$ sudo vi /usr/bin/launchZeal

---
#!/bin/sh
QT_AUTO_SCREEN_SCALE_FACTOR=0 zeal
---
// 저장 후 
$ sudo chmod+x /usr/bin/launchZeal
// 앞으로 launchZeal로 실행이 가능하다.

```
### 한글입력기 [Nimf](https://github.com/janghe11/nimf)
이게 제일 나은듯 
-> https://github.com/hamonikr/nimf
-> https://github.com/hamonikr/nimf/wiki/Manjaro-build
```
$ wget https://github.com/hamonikr/nimf/raw/master/archlinux/nimf-2019.08.14-1-any.pkg.tar.xz
$ sudo pacman -U nimf-2019.08.14-1-any.pkg.tar.xz
```

### [plank독](https://wiki.archlinux.org/index.php/Plank)
깔끔한 독.
```
$ sudo pacman -S plank
```

### [screenkey](https://github.com/wavexx/screenkey)
눌리고 있는 키보드를 화면에 보여줌
```
$ yaourt -s screenkey
```

## alias setting
```
alias vi="vim"
alias oF="~/oF"
alias apps="~/oF/apps"
alias addons="~/oF/addons"
alias pg="projectGenerator"
alias pg.="projectGenerator -tvscode ."
```
