# assignment-1
assignment-1
리눅스 명령어 getopt ,getops
--------------------------------------------------------------------------------------
getopts 유틸리티는 파라메터들의 리스트에서 옵션(options)과 옵션-파라메터(option-parameter)를 추출하는데 사용한다.

getopt = 외부 명령 
getopts = 쉘 내장

사용이유
------------------------
1. 다양한 입력 값이 존재할 경우 사용자와 개발자의 편의를 보장하기 위함 
2. 스크립트를 보다 체계적으로 관리할 수 있기 때문입니다.

'While getopts "a:b:h" opt'

getopt는 첫번째 파라미터로 옵션으로 사용될 문자열을 입력 받고 다음에는 옵션으로 활용되는 변수를 사용

주의할점: ":"이다. 기존적으로 getopt는 한개의 문자만을 구분자로 사용하며 사용할 문자열 뒤에 ":"을 붙이게 되면 뒤에 Value가 붙게 된다는 것을 의미한다.

getopts의 동작 과정
-------------------------
getopts가 호출될 때마다, getopts는 쉘 변수 $name에 다음 옵션 문자를 저장하고, 쉘 변수 $OPTIND에 처리하여야 할 다음 아규먼트에 대한 인덱스를 저장한다. 쉘이 호출 될 때 마다, $OPTIND는 1로 초기화된다.


옵션에서 옵션-아규먼트(option-argument)가 필요한 경우, getopts는 옵션-아규먼트를 쉘 변수 $OPTARG에 저장한다. 분석과정 중에 옵션 아규먼트를 필요로 하는 옵션문자가 없거나, 옵션-아규먼트를 필요로 하는 옵션문자가 있지만 이에 대한 에옵션 아규먼트가 없는 경우에 $OPTARG는 unset된다.


optionstring 오퍼랜드에 포함되지 있지 않은 옵션 문자가 옵션 문자 위치에 있는 경우 name으로 지정된 쉘 변수는 물음표 '?'로 설정된다. 이 경우, optstring의 첫 문자가 콜론 ':'이라면, 쉘 변수 $OPTARG는 발견된 옵션 문자로 설정되며, 표준 에러 출력(stderr)에는 아무 것도 출력되지 않는다. 그 이외의 경우에 쉘 변수 $OPTARG는 unset되고 표준 에러 출력으로 diagonostic message가 출력된다. 이러한 상황은 호출하는 애플리케이션에 아규먼트가 주어지는진 과정에서 탐지된 에러로 볼 수는 있지만, getopts 처리과정에서의 에러는 아니다.

getopts example
--------------------------------
'''
#!/bin/bash
PROGRAM_NAME=`/usr/bin/basename "$0" .sh`

echo shell arg 0 : $0
echo USING BASENAME : ${PROGRAM_NAME} 



global=default
conf=default
svr=default

 

function print_usage() {
/bin/cat << EOF

Usage :
    ${PROGRAM_NAME} [-g global ] [-c config] [-s server]
Option :
    -g, game_initial (L1|AN|BnS)
    -c, config
    -s, server

EOF
}
'''


![getops](https://user-images.githubusercontent.com/87855218/142197931-ea38ebaa-c526-432b-9823-38e9c2eb79ca.png)




![getopts 결과](https://user-images.githubusercontent.com/87855218/142197855-a346c04b-2dce-432f-a135-88a41a88f81c.png)



#sed ,awk 명령어
---------------
sed
-------------------------------------
기본적인 기능은 ed에서 따 왔으며, 이 기능들은 모두 sed에 적용이 된다. 다만 ed는 대화형 편집기이며,
sed는 스트리밍 편집기이다. 대화형 편집기와 스트리밍 편집기의 차이점은 대화형 편집기는 입력 및 출력이
하나로 이루어지며, 스 트리밍 편집기는 하나의 입력이 하나의 출력을 낸다는 것이다.
\n 을 개행문자로 사용하는 스트리밍 에디터이다
|옵션|설명|
| ------ | --- |
|-e script|입력을 처리하는 동안 실행 중인 명령에 스크립트에 지정된 명령을 추가한다.|
|-f file| 입력을 처리하는 동안 실행 중인 명령에 파일에 지정된 명령을 추가한다.|
|-n| 각 명령에 대한 출력을 만들어 내지는 않지만 print명령을 기다린다.|


'sed -n '/abd/p' list.txt : list.txt '
파일을 한줄씩 읽으면서(-n : 읽은 것을 출력하지 않음) abd 문자를 찾으면 그 줄을 출력(p)한다.
'ed 's/addrass/address/' list.txt '
addrass를 address로 바꾼다. 단, 원본파일을 바꾸지 않고 출력을 바꿔서 한다.
'''
sed 's/addrass/address/' list.txt > list2.txt
sed 's/\t/\ /' list.txt 
'''
탭문자를 엔터로 변환


추가(insert)
-----------------------------------
scriptfile - s/


삭제(delete)
-----------------------------------
sed '/TD/d' 1.html 
TD 문자가 포함된 줄을 삭제하여 출력한다.

sed '/Src/!d' 1.html 
Src 문자가 있는 줄만 지우지 않는다.

sed '1,2d' 1.html 
처음 1줄, 2줄을 지운다.

sed '/^$/d 1.html 
공백라인을 삭제하는 명령이다

파 일 이름만을 뽑아내는 정규식
-----------------------------------
s/^.*\/\([a-zA-Z0-9.]*\)".*$/\1/ ^
 라인의 맨 처음, .* 아무문자열, \(, \)은 정규표현식을 그룹화, $ 는 라인의 맨 끝.
 
( s;^.*\/\([a-zA-Z0-9.]*\)".*$;\1;) \1는 그룹화된 첫번째 요소를 말한다.
[a-zA-Z0-9.] 

알파벳과 숫자 및 .(콤마)를 표현하는 문자(character)를 말한다.
즉 GF02.jpg와 같은 문자열을 첫번째 그룹화하고 난 다음 라인 전체를 그룹화된 내용으로 바꾸는 것이다.

/g 
global을 의미 한줄에 대상문자가 여러개일 때도 처리하도록 한다.

who | sed -e 's; .*$;;' 
각 라인의 첫 번째 공백에서부터 마지막까지 삭제하라.

who | sed -e 's;^.* ;;' 
각 라인의 처음부터 맨 마지막 공백까지 삭제하라.

who | sed -e 's;^.*:;;' 
각 라인의 처음부터 : 문자가 있는 곳(:문자포함)까지 삭제하라.

-n 옵션
------------------------------------------------------------
sed는 항상 표준 출력에서 입력 받은 각 라인을 나타낸다는 것을 알아냈다. 그러나 때때로 한 파일로부터 몇 개의 라인들을 추출해 내기 위해 sed를 사용하기를 원할 때도 있다. 이러한 경우에 -n옵션을 사용한다. 이 옵션은 사용자가 만약 해야 할 일을 정확히 말해 주지 않는다면 임의의 라인을 프린트하는 것을 원하지 않는다고 sed에게 말한다. 따라서 p명령이 같이 쓰인다. 라인 번호와 라인 번호의 범위를 나타냄으로써 sed를 사용하여 텍스트의 라인들을 선택적으로 프린트할 수 있게 한다. 다음에서 볼 수 있는 바와 같이, 한 파일로부터 첫 번째 두 라인이 프린트되었다.

' sed -n '1,2p' intro Just print the first 2 lines from intro file.'

만약 라인 번호 대신에 슬래시로 에워 싸인 문자열과 함께 p명령이 쓰인다면 sed는 이들 문자들이 포함하고 있는 표준 입력을 통해서 라인들을 프린트하게 된다. 따라서 하나의 파일로부터 처음의 두 라인을 프린트하기 위하여 다음과 같이 사용될 수 있다.

$ sed -n '/UNIX/p' intro Just print lines containing UNIX

sed '5d' : 라인 5를 삭제

sed '/[Tt]est/d' : Test 또는 test를 포함하는 모든 라인들을 삭제

sed -n '20,25p' text : text로부터 20에서 25까지의 라인들만 프린트

sed '1,10s/unix/UNIX/g' intro : intro의 처음 10개의 라인들의 unix를 UNIX로 변경

sed '/jan/s/-1/-5' : jan을 포함하는 모든 라인들 위의 첫 번째 -1을 -5로 변경

sed 's/...//' data : 각 data라인으로부터 처음 세 개의 문자들을 삭제

sed 's/...$//' data : 각 데이터 라인으로부터 마지막 3문자들을 삭제

sed -n '1' text : 비 프린트 문자들을 \nn으로 (여기서 nn은 그 문자의 8진수 값임),

그 리고 탭 문자들을 > 로 나타내는 각 텍스트로부터의 모든 라인들을 프린트


awk 명령어
--------------------------------------------
awk '/west/' datafile : west 라는 글이 있는 줄 출력

awk '/^north/' datafile : north로 시작하는 줄 출력

awk '/^(no | so)/' datafile : no 또는 so 로 시작하는 줄 출력

awk '{ print $3, $2 }' datafile : datafile 리스트의 세 번째 와 두 번째 필드를 스페이스로 띄어서 출력

awk '{ print $3 $2 }' datafile : datafile 리스트의 세 번째 와 두 번째 필드를 그냥 붙여서 출력

awk '{ print "Number of fields : " NF} ' datafile : datafile의 각 줄마다의 필드수를 리턴한다.

awk '$5 ~ /\.[7-9]+/' datafile : 다섯 번째 필드가 마침표 다음엣 7과 9사이 숫자가 하나 이상 나오는 레코드 출력

awk '$2 !~ /E/ { print $1, $2 }' datafile : 두 번째 필드에 E 패턴이 없는 레코드의 첫 번째와 두 번째 필드 출력

awk '$3 ~ /^Joel/{ print $3 " is a nice guy."} ' datafile : 세 번째 필드가 Joel로 시작하면 " is a nice guy"와 함께 출력

awk '$8 ~ /[0-9][0-9]$/ { print $8 }' datafile : 여덟 번째 필드가 두 개의 숫자이면 그 필드가 출력

awk '$4 ~ /Chin$/ { print "The price is $" $8 "." }' datafile : 네 번째 필드가 Chine으로 끝나면 "The price is $" 8번 필드 및 마침표가 출력

awk -F: '{ print $1 } ' datafile : -F 옵션은 입력 필드를 ':'로 구별.

awk -F"[ :]" '{ print $1, $2 } ' datafile : 입력 필드로 스페이스와 ':'를 필드 구별자로 사용

awk -f awk_script.file datafile : -f 옵션은 awk 스크립트 파일 사용할 때 씀.

awk '$7 == 5' datafile : 7번 필드가 5와 같다면 출력

awk '$2 == "CT" { print $1, $2 }' datafile : 2번 필드가 "CT" 문자와 같으면 1, 2 번 필드 출력

awk '$7 < 5 { print $4, $7}' datafile : 7번 필드가 5보다 작다면 4번, 7번 필드 출력

awk '$6 > .9 { print $1, $6}' datafile : 6번 필드가 .9 보다 크다면 1번, 6번 출력

awk '$8 > 10 && $8 < 17 ' datafile

awk '$2 == "NW" || $1 ~ /south/ { print $1, $2 }' datafile

