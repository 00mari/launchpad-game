# LPHK

다음 문서는 LPHK 깃허브에 올라온 readme.md파일을 정리한 것.



## LPHK란?

* LaunchPad HotKey - (hotkey: 프로그램으로 특정한 기능에 빠르게 접근할 수 있는 단축키.)
* LPHKscript라는 간단한 스크립팅 언어와 GUI를 사용하여 스크립트를 조정할 수 있음.
* 스크립트 기능은 pygame으로 구현됨.

## LPHKscript란?

* 매크로 스크립트 언어

### 스케줄링

* 한 번에 하나의 스크립트만 작동함 -> 스케줄링 시스템 존재.
* 스케줄된(예정된) 스크립트 -> 버튼이 빨간색으로 빛남
* 작동중인 스크립트 -> 버튼이 빨간색으로 깜빡임
* 기능 키의 경우 다르다. 각각 밝은 오렌지 / 빨강
* 예정된 스크립트의 버튼을 눌러서 언스케줄 시킨다.
* 작동중인 스크립트의 버튼을 눌러서 중단시킨다.

### 헤더

@로 시작하는 커맨드는 헤더. 스크립트의 가장 첫 줄에서 써야한다!! 

스크립팅 엔진을 다른 모드로 바꿀 때 쓰인다.

* @ASYNC 헤더
  * 스케줄링 시스템의 예외로서, background에서만 작동하고 다른 스크립트와 상호작용하지 않는다. (버튼을 눌러 취소는 가능)
* @SIMPLE 헤더
  * ???

### 명령어
Commands follow the format: `COMMAND arg1 arg2 ...`. 

Scripts are just a text file with newlines seperating commands.

줄 단위로 구분 

argument = 함수에 전달되는 인자 

* **Utility**
  * `DELAY` 
    * Delays the script for (argument 1) seconds.
  * `GOTO_LABEL`
    * Goto label (argument 1).
  * `IF_PRESSED_GOTO_LABEL`
    * If the button the script is bound to is pressed, goto label (argument 1).
  * `IF_PRESSED_REPEAT_LABEL`
    * If the button the script is bound to is pressed, goto label (argument 1) a maximum of (argument 2) times.
  * `IF_UNPRESSED_GOTO_LABEL`
    * If the button the script is bound to is not pressed, goto label (argument 1).
  * `IF_UNPRESSED_REPEAT_LABEL`
    * If the button the script is bound to is not pressed, goto label (argument 1) a maximum of (argument 2) times.
  * `LABEL`
    * Sets a label named (argument 1) for use with the `*GOTO_LABEL` commands.
  * `OPEN`
    * Opens the file or folder (argument 1).
  * `REPEAT_LABEL` (라벨이름, 반복횟수)
    * Goto label (argument 1) a maximum of (argument 2) times.
  * `RESET_REPEATS` (인자 없음)
    * Reset the counter on all repeats. (no arguments)
  * `SOUND` (파일명, (볼륨))
    * Play a sound named (argument 1) inside the `user_sounds/` folder.
      * Supports `.wav`, `.flac`, and `.ogg` only.
    * If (argument 2) supplied, set volume to (argument 2).
      * Range is 0 to 100
  * `WAIT_UNPRESSED`
    * Waits until the button the script is bound to is unpressed. (no arguments)
  * `WEB`
    * Open website (argument 1) in default browser.
  * `WEB_NEW`
    * Open website (argument 1) in default browser, try new window.
* **Keypresses** 키보드
  * `PRESS` (버튼이름)
    * Presses the key (argument 1).
      * 이용 가능한 키보드 버튼 목록은 아래에
      * press는 tap이랑 다른 개념. 즉, release가 없는 한 계속 누르고 있음.
  * `RELEASE`
    * Releases the key (argument 1).
      * See valid key names below.
  * `RELEASE_ALL`
    * Releases all pressed keys, including those pressed by other scripts. (no arguments)
  * `STRING`
    * Types whatever text comes after it.
  * `TAP` (키 이름, (횟수), (반복마다 딜레이되는 초))
    * Taps the key (argument 1).
      * See valid key names below.
    * If (argument 2) supplied, tap (argument 2) number of times.
    * If (argument 3) supplied,  delay (argument 3) seconds before releasing each time.
* **Mouse Movement** 마우스
  * `M_LINE` (x1, y1, x2, y2, (딜레이*), (한번에 몇픽셀 움직일 것인지?))
    * Move the mouse in a line from absolute point (argument 1),(argument 2) to absolute point (argument 3),(argument 4).
    * If (argument 5) supplied, delay (argument 5) milliseconds between each step.
    * If (argument 6) supplied, move (argument 6) pixels per step.
      * If not supplied, assumed to be 1
  * `M_LINE_MOVE`
    * Move the mouse cursor in a line (argument 1) horizontally and (argument 2) vertically, relative to current position
    * If (argument 3) supplied, delay (argument 3) milliseconds between each step.
    * If (argument 4) supplied, move (argument 4) pixels per step.
      * If not supplied, assumed to be 1
  * `M_LINE_SET`
    * Move the mouse cursor in a line to absolute point (argument 1),(argument 2)
    * If (argument 3) supplied, delay (argument 3) milliseconds between each step.
    * If (argument 4) supplied, move (argument 4) pixels per step.
      * If not supplied, assumed to be 1
  * `M_MOVE`
    * Moves the mouse cursor (argument 1) horizontally and (argument 2) vertically, relative to current position.
  * `M_RECALL`
    * Sets the mouse position to the last location stored with `M_STORE`.
      * Will not do anything if `M_STORE` has not been called in that script.
  * `M_RECALL_LINE`
    * Move the mouse cursor in a line to the last location stored with `M_STORE`.
      * Will not do anything if `M_STORE` has not been called in that script.
    * If (argument 1) supplied, delay (argument 1) milliseconds between each step.
    * If (argument 2) supplied, move (argument 2) pixels per step.
      * If not supplied, assumed to be 1
  * `M_SCROLL`
    * Scrolls the mouse vertically by (argument 1).
    * If (argument 2) supplied, scroll horizontally by (argument 2).
  * `M_SET`
    * Sets the absolute cursor posistion to (argument 1) horizontal and (argument 2) vertical.
  * `M_STORE`
    * Stores the current mouse position for use with the `M_RECALL*` commands.

For the `PRESS`, `RELEASE`, and `TAP` commands, all single character non-whitespace keys and the following key names are allowed:
* `alt`
* `alt_gr`
* `backspace`
* `caps_lock`
* `cmd`
* `ctrl`
* `delete`
* `down`
* `end`
* `enter`
* `esc`
* `f1` - `f24`
* `home`
* `insert`
* `left`
* `menu`
* `mouse_left`
* `mouse_middle`
* `mouse_right`
* `mute`
* `next_track`
* `num_lock`
* `page_down`
* `page_up`
* `pause`
* `play_pause`
* `prev_track`
* `print_screen`
* `right`
* `scroll_lock`
* `shift`
* `shift_r`
* `space`
* `tab`
* `up`
* `vol_down`
* `vol_up`

For all commands, the arguments cannot contain the following strings, as they are reserved for the LPHKlayout file format:
* `LPHK_BUTTON_SEP`
* `LPHK_ENTRY_SEP`
* `LPHK_NEWLINE_REP`
