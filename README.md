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
## 프린터 세팅
-> [https://wiki.manjaro.org/index.php?title=Printing](https://wiki.manjaro.org/index.php?title=Printing)
### Brother HL-1210W
#### 드라이버 설치 및 프린터 매니저 설치 (없을경우)
```
$ yaourt -s 1210w
$ yaourt -s print-manager
```
#### 프린터 추가하기
- 서비스 등록을 위해 사용자를 sys그룹에 추가
```
$ sudo gpasswd -a yourusername sys
```
- Device URL : `socket://[PRINTER_IP_ADDRESS:9100]`
- 드라이버 : 설치한 드라이버 선택
- 테스트 인쇄 해보기

## 유용한 유틸리티
### AUR (deprecated.. not recommand)
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

### yay (AUR alternative)
-> [https://github.com/Jguer/yay](https://github.com/Jguer/yay)
```
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
### 마우스 휠클릭 붙여넣기 끄기
-> [stackExchange.com](https://unix.stackexchange.com/questions/24330/how-can-i-turn-off-middle-mouse-button-paste-functionality-in-all-programs)

```
$ pacman -S xbindkeys xsel xdotool
```

```
$ vi ~/.xbindkeysrc
---
"echo -n | xsel -n -i; pkill xbindkeys; xdotool click 2; xbindkeys"
b:2 + Release
---
```
then reload `xbindkeys -p`\
run `xbindkeys` on startup, `pkill xbindkeys` to stop


### oh-my-zsh
```
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
### others
```
$ sudo pacman zsh vim terminator 
$ yay -s vscode  #visual studio code
$ yay -s iosevka-term #iosevka ttf font
$ yay -s minetime #google calendar
$ yay -s ncspot # spotify on terminal
```
### [rofi](https://github.com/DaveDavenport/rofi)
스팟라이트/alfred와 같은 간단 런처
```
$ sudo pacman -S rofi
```
- 테마 선택 : `rofi-theme-selector` 로 선택 후 `alt+a`
- keyboard shortcut command : `rofi -show drun`
- theme confdig
```
$ vi ~/.config/rofi/config
==============

rofi.theme: Monokai
rofi.font:  Iosevka Term Medium 11
rofi.modi:  drun
```

### [zeal](https://github.com/zealdocs/zeal)
오프라인 도큐먼트 문서. dash for mac과 같다. \
Qt관련 버그가 있는듯. 예전엔 HiDPI 관련 이슈로 아이콘등이 이상하게 크기가 이상하더니, 아에 구동이 안되기도 한다.\

github에서 직접 소스를 받아 빌드하여 실행하고, 쉘 스크립트를 만들어 QT옵션을 주며 실행토록 한다.
```
$ git clone https://github.com/zealdocs/zeal
$ cd zeal
$ mkdir build && cd build
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
### terminator color setting
- pre-requirements
 ```
$ sudo pacman -S python2-pip
$ sudo pip2 install requests
 ```
-> [terminator-themes](https://github.com/EliverLara/terminator-themes)


### 한글입력기 [Nimf](https://github.com/janghe11/nimf)
이게 제일 나은듯 
-> https://github.com/hamonikr/nimf
-> https://github.com/hamonikr/nimf/wiki/Manjaro-build
```
$ wget https://github.com/hamonikr/nimf/raw/master/archlinux/nimf-2019.08.14-1-any.pkg.tar.xz
$ sudo pacman -U nimf-2019.08.14-1-any.pkg.tar.xz
```
```
vi ~/.xprofile

export GTK_IM_MODULE=nimf
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE=nimf
export XMODIFIERS="@im=nimf"
nimf

```

### [plank독](https://wiki.archlinux.org/index.php/Plank)
깔끔한 독.
```
$ sudo pacman -S plank
```

### [screenkey](https://github.com/wavexx/screenkey)
눌리고 있는 키보드를 화면에 보여줌
```
$ yay -s screenkey
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
## NVIDIA CUDA setup
```
$ yaourt -s cuda
> select (cuda cudnn) with installed nvidia driver version (opencl-nvidia-XXXxx)
```
## OF 0.11.0 setup
### ALCdevice error
-> https://forum.openframeworks.cc/t/compilation-failing-due-to-confliting-definition-in-openal/33927/2
> A fix for this which we should do on our end ( and should work with both old and new releases ) should be:
```
$ vi ~/oF/libs/openFrameworks/sound/ofOpenALSoundPlayer.h
```
```
typedef struct ALCdevice_struct ALCdevice;
/** Opaque context handle */
typedef struct ALCcontext_struct ALCcontext;

to:

struct ALCdevice;
struct ALCcontext;
```
## known bug
### notifyd service not running
```
$ systemctl --user start xfce4-notifyd
$ systemctl --user status xfce4-notifyd
$ systemctl --user enable xfce4-notifyd
```
