# 웹 취약점 분석과 시큐어코딩 (2026.11)

# 1일차

## 1.1 실습용 프로그램 다운로드

## https://github.com/nadopro/kpc2611

[github 실시간 코드 배포](https://github.com/nadopro/kpc2611)

[download xampp](https://www.google.com/search?q=download+xampp&oq=download+xampp&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIGCAEQABgeMgYIAhAAGB4yBggDEAAYHjIGCAQQABgeMgYIBRAAGB4yBggGEAAYHjIGCAcQABgeMgYICBAAGB4yBggJEAAYHtIBCTM4ODNqMGoxNagCCLACAQ&sourceid=chrome&source=chrome.rb&ie=UTF-8)

> 실행할 때 "Windows의 PC 보호" 파란 창이 뜨면,  
> "추가정보" 클릭 후, 실행  
> 기본 설정, 설치 위치 c:/xampp  

[download visual code](https://www.google.com/search?q=download+visual+code&sca_esv=c0e41f13f2bcea41&sxsrf=AKL5yDirYY0Z88GN1X9mjGqp8aZVOsPQuQ%3A1794786927285&ei=b0b6as72EOvk2roP5JW12Qs&biw=1289&bih=566&uact=5&oq=download+visual+code&gs_lp=Egxnd3Mtd2l6LXNlcnAiFGRvd25sb2FkIHZpc3VhbCBjb2RlMgUQABiABDIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHjIEEAAYHkiBMVCTF1ioMHACeAGQAQCYAWSgAckIqgEEMTEuMbgBA8gBAPgBAZgCDqACvAnCAgoQABhHGNYEGLADwgIXEC4Y3AYYuAYY2gYY2AIYyAMYsAPYAQHCAgoQABiABBiKBRhDwgIGEAAYHhgKmAMAiAYBkAYQugYGCAEQARgZkgcDNy43oAf_QbIHAzUuN7gHqgnCBwcwLjUuNS40yAdMgAgB&sclient=gws-wiz-serp)

### 1.1.1 설치 확인
- [http://localhost](http://localhost)

- [http://localhost/phpmyadmin](http://localhost/phpmyadmin)

**만약 mysql 사용자 계정 추가가 안되는 경우**

- [X] 계정 추가 안될때
- [X] curl을 이용한 크롤링 안될 때

> 환경 변수에 추가
> 시스템 변수 -> Path -> 새로 만들기(N)
> c:/xampp/php
>

C:\xampp\phpMyAdmin\config.inc.php 파일의 아래와 같이

cookie 부분 수정, 

DisableIS 부분 추가

후, Apache 재시작

```php
<?php
/* Authentication type and info */
$cfg['Servers'][$i]['auth_type'] = 'cookie'; // 수정
$cfg['Servers'][$i]['user'] = 'root';
$cfg['Servers'][$i]['password'] = '';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['AllowNoPassword'] = true;
$cfg['Lang'] = '';
$cfg['Servers'][$i]['DisableIS'] = true; // 추가
?>
```
### 1.1.2 기타 프로그램 

[download burp suite community edition](https://www.google.com/search?q=download+burp+suite+community+edition&oq=download+burp+suite+&gs_lcrp=EgZjaHJvbWUqBwgBEAAYgAQyCAgAEEUYHhg5MgcIARAAGIAEMgYIAhAAGB4yBggDEAAYHjIGCAQQABgeMgYIBRAAGB4yBggGEAAYHjIGCAcQABgeMgYICBAAGB4yBggJEAAYHtIBCDk4MzlqMGo0qAIAsAIB&sourceid=chrome&source=chrome.ob&ie=UTF-8)

[download zaproxy](https://www.zaproxy.org/)


## 2. Regular Expression

```
    [abc]  : a, b, c 중에 하나  
    ls *.[ch]  
    [abc]{2} : a, b, c중에서 골라서 2개
    ac, cc, ca, da  
    [abc]{2,4} : 2~4글자
    aaa, aca, bca
    [abc....xyz]{4,10}
    test, desktop, secure
    [a-zA-Z0-9]{4,10}
    Test, Test12, abcd343

    ^010-[0-9]{4}-[0-9]{4}$
    010-123a-5678Test010-1111-2222Test

    Uni + code
    1B : 256
    2B : 65536
    한국어 : 됬다 -> 됐다
    문법 : 3400자.
    조합가능 : 11000자

    한글은 국어사전에 나열된 순서대로 번호를 부여

    AC00 : 가
    AC01 : 각
    AC02 : 갂
    AC03 : 갃
    ...
    LAST : 힣

    ^[가-힣]{2,4}$

    3B : 1600만
    4B : 40억

match, mapping, mother, mat
홍길동 이순신 세종대왕 a강b감c찬
전화번호010-1a11-1111010-1234-5678test
match, mapping, mother, 
홍길동 이순신 세종대왕 a강b감c찬
전화번호010-1a11-1111010-1234-5678test
match, mapping, mother, 
홍길동 이순신 세종대왕 a강b감c찬
전화번호010-1a11-1111010-1234-5678test

```

* SQL Injection *
```
    프로그래머들의 습성을 이용

    $id = "test";
    $pass = "1111";

    $sql = "select * from users where id='$id' and pass='$pass' ";


    "select * from users where id='test' and pass='1111' ";
    id : xxx' or 2>1 limit 1, 1 -- 
    pass : zzz 
    "select * from users where id='xxx' or 2>1 1, 1 -- ' and pass='zzz' ";

```
* 용어 설명 *

> X : Ex, Windows Expert  
> XML : Ex  
> X : Cross Site Scripting : XSS  
> X : AI Transmission, Xmit  
> N : En, Nginx  


## 3. 홈페이지 구조 (index.php, db.php)

모든 파일은 index.php 파일을 통과

* Q1 : 골격 *
```
다음을 만족하는 index.php 파일을 만들어줘.
HTML5와 Bootstrap5를 이용해 반응형 홈페이지를 만들거야.
상단에는 Navbar를 이용해서 메뉴를 구성할거야.
메뉴에는 menu1, menu2, menu3이 있어.
menu1에는 menu1-1, menu1-2, menu1-3,
menu2에는 menu2-1, menu2-2,
menu3에는 menu3-1, menu3-2로 dropdown형태로 구성할거야.

내용(body) 부분에는 하단의 cmd 결정에 의해 화면을 표시할거야.
하단에는 사이트 정보가 있는데,
"한국생산성본부(KPC)
정보보호책임자: 홍길동(help@kpc.or.kr)"
이렇게 구성되어 있어.

만약에 내용이 너무 적더라도 하단의 사이트정보는 항상 화면의  맨 아래에 배치되도록 구성해 줘.

메뉴부분은 진한 파스텔톤의 녹색 계열로 만들고,
화면은 연한 파스텔톤 녹색 계열로 만들고 싶어.

맨 앞에서는 db.php파일을 추가해 줘.
db.php 파일은 mysql에 접속하는 코드를 함수형태로 만들거야.
index.php에서는 다음과 같이 호출해서 접속을 한번에 해결할거야.
$conn = connectDB(); 

connectDB()를 위해서
$db name = secure
$db user = secure
$db pass = 1111

mysqli()를 사용할거야.

모든 파일은 index.php?cmd=test 와 같은 형태로 cmd값으로
동작을 결정할거야.

GET방식으로 넘어온 $cmd가 없으면
기본값으로 init.php를 본문에 포함할거야.
만약 cmd=test이면 test.php 파일을 추가하도록 코드를 만들거야.

init.php 파일은 일단 다음과 같이 구성할거야.

KPC 보안 프로그래밍 과정

```

**Q2: users table schema 만들기**
```
    mysql 테이블 스키마를 만들고 싶어.
    table name : users
    필요한 정보 : idx, id, name, pass, level
    idx : 정수, 자동증가, primary key
    id : text, unique,
    name : 사용자 이름,
    pass : 50글자의 텍스트, 암호화 하지 않음
    level : 1(일반회원), 2(우수회원), 중간 번호는 예비, 9(관리자)

    1. 스키마를 만들어줘.
    2. 아이디 10개를 만드는 query를 만들어줘.
    admin(관리자), test(테스트)
    나머지는 조선시대 역사 인물 이름으로 무작위로 만들어줘. 모든 비밀번호는 abcd로 세팅하고,
    관리자만 9번, 나머지는 1번을 level로 세팅해
```
**결과**
```sql
CREATE TABLE users (
    idx INT NOT NULL AUTO_INCREMENT,
    id VARCHAR(50) NOT NULL,
    name VARCHAR(100) NOT NULL,
    pass VARCHAR(50) NOT NULL,
    level TINYINT UNSIGNED NOT NULL DEFAULT 1,
    PRIMARY KEY (idx),
    UNIQUE KEY uk_users_id (id),
    CONSTRAINT chk_users_level
        CHECK (level BETWEEN 1 AND 9)
) ENGINE=InnoDB
  DEFAULT CHARSET=utf8mb4
  COLLATE=utf8mb4_unicode_ci;


  INSERT INTO users (id, name, pass, level) VALUES
('admin',      '관리자',   'abcd', 9),
('test',       '테스트',   'abcd', 1),
('sejong',     '세종대왕', 'abcd', 1),
('yi_sunsin',  '이순신',   'abcd', 1),
('jeong_yakyong', '정약용', 'abcd', 1),
('heogjun',    '허준',     'abcd', 1),
('shinsaimdang', '신사임당', 'abcd', 1),
('kim_hongdo', '김홍도',   'abcd', 1),
('janggyeong', '장영실',   'abcd', 1),
('hwangjini',  '황진이',   'abcd', 1);
```

* Q3: cmd 체크 *
```
조금전 index.php 다음과 같이 수정했어.
$pages = [
    '시큐어코딩' => ['injection', 'injection2', 'injection3'],
    'menu2' => ['menu2-1', 'menu2-2'],
    'menu3' => ['menu3-1', 'menu3-2'],
];


이때, injection.php파일을 만들어야 해.
users 테이블에서 아이디와 비번이 같은지 로그인하는 화면이야.

id, pass를 입력받아서 "로그인"을 수행하면, 
조금 전 만들었던 users 테이블과 비교하는거야.
injection.php 파일은 mysqli_query()와 같은 함수로 질의 하고 싶고, 인젝션 공격을 테스트하기 위한 코드를 만드는 것이 목적이야.

$sql = "select * from users where id='$id' and pass='$pass' "; 와 같은 형식의 코드를 사용해 줘.

index.php 파일에서 세션을 저장하기 위해 sess라는 폴더를 만들었어.
id, name, level
즉 세션처리를 위해 index.php파일과 injection.php 파일을 제시해 줘.
injection.php 파일에는 로그아웃 버튼까지 동작하도록 해 줘.
```
**세션확인**

주소창 

javascript:alert(document.cookie);

**성능**
```
connectDB();

for(; ;)
{
    insert into ...();
}

close()


for(; ;)
{
    connectDB();
    insert into ...();
    close();
}


char *p = (char *) malloc(1000);
free(p);

if(p)
{
    printf("Yes");
}else
{
    printf("No");
}


for(i)
{
    fopen(i.txt)
}
```

**Q3 : save id**

```
(injection2.php 첨부)
첨부한 파일을 수정해서, id, pass를 저장하는 기능을 만들고 싶어.
목표 파일은 saveid.php 이야.
저장한 아이디와 비밀번호는 localStorage에 저장하고 싶어.
체크박스로 저장기능을 선택하도록 saveid.php 파일을 제시해 줘.
```


# 2일차

## 2.1 IP Address

```
1.2.3.4 : 0.0.0.0 ~ 255.255.255.255

첫자리
A class
0000 0000 ~ 0111 1111 : 0~127

100.*.*.* : 1,600만
Special Purpose : 10.*.*.*, 127.*.*.*(loop back)

B class
10xxx : 1000 0000 ~ 1011 1111 : 128~191
153.14.*.* : 65,536
SP: 172.*

C class
11xx : 1100 0000 ~ 1101 1111 : 192 ~ 220

200.54.13.*
SP : 192.168.*.*

200.100.13.*

200.100.13.0 : 방 이름(network name)
200.100.13.255 : broadcast address, 방송

```

**C code**
```c
void copy(char *ptr) {
    char buf[100];
    strcpy(ptr, buf);
    printf("buf = %s\n", ptr);
    print(buf);
}
// ./test "Hello World"
// ./test $(python print("A"* 10 + "B" * 20))
int main(int argc, char **argv) {
    copy(argv[1]);
}

a()
    a1()
        a11()
    a2()
b()
    b1()
    b2()
```

**유선인터넷과 무선인터넷**

```
유선 인터넷

고속 인터넷 -> 초고속 인터넷 -> 광인터넷
ADSL : Asymetric Digital Subscriber Line 
    Up/Down load 의 비대칭

무선 인터넷
1G -> NG(2G) -> 3G(iPhone, 010 통합)
3.5G : 영상통화, KT Show, SKT T, LGT oz
4G : LTE, 목표(FHD), mp4
    LET-A : 무선 속도 > 유선 속도
5G : 목표(UHD)
6G : 1G/sec, 자율주행 자동차

Netmask

2*2*2 , 2<<2

    0010
    0100 : 4
    1000 : 8

    1.2.3.4 : 0000 0001

    0001.0010.0011.0100
    1111.1111.1111.0000
   &   1.   2.   3. 0  

    0001.0010.0011.0110
    1111.1111.1111.0000
   &   1.   2.   3. 0    

    0001.0010.0111.0101
    1111.1111.1111.0000
   &   1.   2.   7. 0   

   256-32 = 224
   255.255.255.224


    ChatGPT : Chat, Generative Pretrained Transformer
```


**Q4 : save id, 암호화**

```
(saveid.php 첨부)
첨부한 파일은 정상적으로 잘 동작하고 있어.
그런데, 이 코드를 개선하고 싶어.
비밀번호가 저장될 때, localStorage에서 비밀번호가
노출되는 문제가 있어.
암호화해서 저장하고,
입력창으로 가져올때는 복호화해서 ****처럼 보여주고 싶어.
또, 로그인 실행할 때, 패킷을 web proxy로 검사하면
raw 데이터가 노출되는 문제가 있어.
패킷으로 날라갈때는 다시 암호화(인코딩)하고,
DB와 검사할때는 복호화해서 검사하도록 로직을 변경해 줘.
저장되는 파일이름은 saveid2.php 야.
```

**JSON**
```
JavaScript Object Notation  
<img src="a.jpg" width="100">  
width:100  

key:value

{} : 객체  
[] : 배열, 리스트, 목록  

{
    "name":"홍길동",
    "age":12, 
    "company":"KPC"
}

{
    "name":"홍길동",
    "age":12, 
    "company": {
        "name": "KPC",
        "url" : "http://kpc.or.kr",
        "tel" : "02-1111-2222"
    }
}

{
    "person": {
        "name":"홍길동",
        "age":12
    }, 
    "company": {
        "name": "KPC",
        "url" : "http://kpc.or.kr",
        "tel" : "02-1111-2222"
    }
}

{
    "직원": [
        {"name":"홍길동", "age":12}, 
        {"name":"이순신", "age":15}, 
        {"name":"이도", "age":54}
    ], 
    "company": {
        "name": "KPC",
        "url" : "http://kpc.or.kr",
        "tel" : "02-1111-2222"
    }
}

{
    "nodes": [
        {"id":"홍길동"},
        {"id":"이이"},
        {"id":"사임당"}
    ],
    "links": [
        { "src":"사임당", "target":"이이", "rel":"모자"},
        { "src":"홍길동", "target":"이이", "rel":"친구" }
    ]
}


{
    "q":"네트워크보안에 대해서 알려줘.",
    "detail": [

    ]
}
```

**Q5: JSON만들기**
d3js : Data Driven Document

https://d3js.org
```
인물관계를 JSON으로 표시하고 싶어.
노드와 링크로 구성되어 있어.
노드는 인물, 링크는 관계야.

신사임당의 아들: 이율곡,
홍대감의 아들:홍길동
이율곡의 친구: 홍길동
이순신의 친구: 유성룡
이순신의 선생님: 이율곡
```

**Q5: JSON으로 관계망 만들기**

```
지금 만들어진 JSON 데이터를 이용해서, 
HTML5와 d3js를 이용해서 네트워크 다이어그램으로 그리고 싶어.
노드는 원으로 표시하고, 안에는 텍스트로 이름을 적어줘.
관계는 직선으로 표시하는데,
부모-자식관계: 빨간색
친구: 파란색
사제관계: 검정색

선의 두께는 4px로 그려줘.
이때, 마우스의 휠의 동작에 따라 확대/축소하고 싶어.
만약 오른쪽 마우스를 누르면 이동을 하고 싶어.

선에다 마우스를 올리면 둘 사이의 관계를 텍스트로 확인할 수 있도록 해줘.
index.php?cmd=relation으로 사용하기 위해
relation.php파일을 만들어줘.
```

**Q6: 무차별대입공격 brute force attack**

```
cmd=brute에서 동작하는 brute.php파일을 만들거야.
영문으로 된 텍스트를 찾는 원리를 코드로 만들고 싶어.
예를 들어 4자리수 비밀번호를 찾고 싶어.
aaaa,aaab, aaac,aaad,... zzzz까지 검사하는 코드야.
users 테이블의 비밀번호와 이 텍스트가 같은지 비교하는 코드를 만들고 싶어.
만약에 하나라도 찾으면, 동일한 비밀번호를 갖는 아이디와 이름을 모두 출력하고 프로그램을 종료해줘.
결과는 표형태로 정리해 줘.
표의 열은 순서, 아이디, 이름, 비밀번호로 정리해 줘.
만약 반복문을 사용하는 경우에, 
반복문이 1000회 수행될 때마다, 화면에 횟수를 출력해 줘.
최종적으로 몇 번만에 찾았는지도 출력해 줘.
```

**Q7 : Web Shell**

```
같은 방법으로 shell.php을 만들고 싶어.
사용자 입력으로 command를 입력받고, 실행버튼을 누르면
하단에 명령을 수행하도록 해 줘.
만약에 화면에 출력하는 과정에서 한글이 깨지는 현상이 없도록 인코딩 처리도 해 줘. 


netstat -an
```

# 3일차

## 3.1 Log

- Log을 위한 테이블 생성

```
1.2.3.4 ==> SKB, GPS
다음과 같은 Mysql 스키마를 만들고 싶어.
table name : log
필드 정보
 idx: integer, auto_increment, primary key
 ip: ipv4 주소
 id: 사용자의 아이디
 work:varchar(255)
 time: datetime
```

**결과***
```sql
CREATE TABLE log (
    idx INT NOT NULL AUTO_INCREMENT,
    ip VARCHAR(15) NOT NULL,
    id VARCHAR(100) NOT NULL,
    work VARCHAR(255) NOT NULL,
    time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (idx)
) ENGINE=InnoDB
  DEFAULT CHARSET=utf8mb4
  COLLATE=utf8mb4_unicode_ci;
```


**iot**

```
mysql 스키마를 만들어줘.
table name : iot
idx: integer, auto increment, primary key
temp : float
hum : float
time : datetime
```
**결과**
```sql
CREATE TABLE iot (
    idx INT NOT NULL AUTO_INCREMENT,
    temp FLOAT DEFAULT NULL,
    hum FLOAT DEFAULT NULL,
    time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (idx)
) ENGINE=InnoDB
  DEFAULT CHARSET=utf8mb4
  COLLATE=utf8mb4_unicode_ci;
```

**시뮬레이터**

```
$tem = rand(250, 260) /10
gen.php파일을 만들고 싶어.
랜덤하게 온도와 습도를 발생하고 싶어.
온도는 25-26도 사이,
습도는 70-71% 사이
랜덤하게 발생 두 값을 직전에 만든 iot 테이블에 넣는 작업을 할거야.
자바스크립트로 3초마 setTimeout()을 활용해서
반복적으로 작업을 하고 싶어.
```

**monitor**
```
이번에는 생성된 iot로그를 그래프로 보여주는 monitor.php를 만들고 싶어.
구글차트의 라이차트를 이용해서 iot테이블의 온도, 습도를 같이 출력하고 싶어.
그런데, 데이터가 많아지는 것을 대비하기 위해
최근 100개만 보여주고 싶어.
즉 만약 데이터가 1000개가 있다면, 901~1000까지만 보고 싶어.
지속적으로 모니터링을 하기 위해 3초마다 한번씩 새로고침해줘.
```

**회원가입(ajax)**

```
첨부한 것과 같이 users테이블의 구조가 있는데, 
join.php에서 회원가입하는 기능을 만들고 싶어.
id는 중복검사를 해야하는데, 이를 위해
아이디의 키가 입력될 때마다 ajax로 요청해
입력된 id의 사용 가능/불가능 여부를 판단하고 싶어.
4글자 미만일 때는 "아이디는 4글자 이상입니다."라고 표시해.
가능/불가능 여부를 화면에 출력도 해 줘.
사용 가능한 아이디이면 "회원가입"버튼을 활성화해줘.
사용불가능하면 버튼을 비활성화해줘.
level은 무조건 1번이기 때문에 별도로 입력받을 필요가 없다.
비밀번호는 두번 입력받아야 해.
회원가입을 하는 경우, 실제로 가입까지 해줘.
```

WYSIWYG : What You See Is What You Get

```
editor.php 파일을 만들고 싶어.
게시판의 글쓰기 화면을 만들건데,
WYSYWIG 게시판 형태로 만들거야.
Bold, Italic, Underline 만 샘플로 만들거야.
이 세개의 버튼은 Material-icons를 활용해 줘.
```

**게시판 스키마**

```
게시판을 만들고 싶어.
table: board
filed는 다음과 같아.
idx : integer, auto increment, primary key
id : 작성자 id
name : 작성자 이름
gid : 게시글의 그룹번호
thread: 그룹내에서 구분하기 위한 텍스트
title : 게시판 제목
notice : 1, 0 공지사항 여부
content : 게시판 내용(plain text)
hit : 읽은 횟수, 기본값 0
file : 첨부파일이름
fname: 파일의 원본이름 
time : datetime
```

**결과***
```sql
CREATE TABLE board (
    idx INT NOT NULL AUTO_INCREMENT,
    id VARCHAR(100) NOT NULL,
    name VARCHAR(100) NOT NULL,
    gid INT NOT NULL DEFAULT 0,
    thread VARCHAR(255) NOT NULL DEFAULT '',
    title VARCHAR(255) NOT NULL,
    notice TINYINT(1) NOT NULL DEFAULT 0,
    content LONGTEXT DEFAULT NULL,
    hit INT UNSIGNED NOT NULL DEFAULT 0,
    file VARCHAR(255) DEFAULT NULL,
    fname VARCHAR(255) DEFAULT NULL,
    time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,

    PRIMARY KEY (idx),
    INDEX idx_gid_thread (gid, thread),
    INDEX idx_time (time)
) ENGINE=InnoDB
  DEFAULT CHARSET=utf8mb4
  COLLATE=utf8mb4_unicode_ci;

alter table board add ip char(20) default '0.0.0.0';

```

```
만들어진 테이블에 게시글 3개를 작성해줘.
작성자: admin, 이름 : 관리
제목 : 테스트 제목1 ~ 테스트 제목3
내용: 테스트 내용1 ~ 테스트 내용3
gid = 1, 2, 3
thread= 모두 A

INSERT INTO board
    (id, name, gid, thread, title, content)
VALUES
    ('admin', '관리', 1, 'A', '테스트 제목1', '테스트 내용1'),
    ('admin', '관리', 2, 'A', '테스트 제목2', '테스트 내용2'),
    ('admin', '관리', 3, 'A', '테스트 제목3', '테스트 내용3');
```

**게시판 만들기**
```
조금 전 제시한 스키마에
alter table board add ip char(20) default '0.0.0.0';
이렇게 추가했어.
board.php파일을 다음 조건에 맞춰 만들어 줘.
index.php?cmd=board와 같이 사용하는데,
게시판의 기능을 위해 mode를 사용할거야.
index.php?cmd=board&mode=show 와 같은 형태로 동작을 결정해.
mode가 없는 경우에는 mode="list"를 기본으로 해줘.
동작에는 
목록보기(mode = list), 내용보기(mode = show),
글쓰기(mode = write), 삭제하기(mode=delete) 등이 있어.

1. 글목록 보기
순서, 제목, 작성자, 파일, 작성일, 읽음 이 표형태로 출력돼.
스마트폰 같은 디바이스에서는 제목과 작성자만 보여줘.
내용을 클릭하면 글보기로 이동해.
화면 하단에는 "글쓰기" 버튼이 있고, 클릭하면 글쓰기로 이동해. 한페이지당 10개씩 보여주고, 그 이상일때는 pagenation으로 표시해 줘.

2. 글쓰기(mode =write)

제목, 
작성자,
내용, 첨부 기능이 있어.
만약 관리자인 경우는 "공지"를 선택할 수 있어야 해.
맨 아래에는 <목록> 버튼이 있어. <등록> 버튼이 있어.
등록 버튼을 누르면 정의한 스키마에 맞게 등록해 줘.
만약 첨부한 파일이 "테스트.jpg"라면
저장할 때 중복을 피하기 위해 20261118123456.jpg와 같이 바꾸고 싶어. 즉, YYYYmmddHHMMss.jpg와 같은 형태야.
file에는 "날짜정보.확장자", fname에는 원본 이름인 "테스트.jpg"가 저장돼.
gid는 새글을 기준으로 순차적으로 1번부터 증가해.
thread는 원본글 새글은 "A"야.
댓글은 달리는 순서대로 AA, AB, AC와 같이 원본글에 대한 몇번째 글인지 구분하고 싶어.
만약 AB에 댓글이 두개 달리면 ABA, ABB
A에 댓글이 달리는 순서대로 AA, AB, AC, AD..
ABC에는 ABCA, ABCB, ABCC,... 

목록을 가져올 때 order by notice desc, gid desc, threa asc 순으로 가져오고 싶은거야.


3. 글보기(mode = show)
제목이 첫줄, 공지사항 여부는 제목 앞에 표시
두번째 줄에는 작성자, 작성일을 보여주고, 
관리자인 경우에는 ip주소까지 출력해 줘.
내용을 출력하는데,내용밑에 첨부한 파일이 이미지파일인 경우에는 화면에 보여줘.
하단에는 첨부파일을 다운로드할 수 있게 해 줘.
이전글, 다음글로 이동할 수 있게 해줘.
<목록> <답글>버튼이 있고,
글쓴사람이나 관리자인 경우에는 <수정><삭제>버튼을 만들어줘.

4. 수정하기

update를 할 것이기 때문에 uidx=3이면 3번 글을 수정한다는 의미야.
수정하기를 할 때, 글쓰기하는 화면을 그대로 이용해 줘.
단지 uidx의 여부로 새글과 수정하는 글을 구분하면 돼.

5. 답글달기
답글달기는 reply라는 의미로 ridx를 사용할거야.
같은 방법으로 글쓰기 화면을 그대로 이용할거야.

만약에 원본글이

"하나
둘"
이라면

"


>> 하나
>> 둘
"
이렇게 표시해야 하는데, 정규식을 활용해서 처리하면 돼.

삭제할 때는 다음과 같이 꼭 물어봐줘.
"삭제한 글은 복구할 수 없습니다.
"정말 삭제하시겠습니까?"


```

點數 , 壓卷

**dice**

```
랜덤이 정확하게 분포하는지 프로그램으로 만들고 싶어.
$dice[1] ~$dice[6] 0으로 초기화해.

사용자로부터 값을 입력받고 실행하면 동작하는 구조야.
사용자 입력은 숫자로 입력받고, 기본값은 6
입력 값만큼
무작위로 rand(1, 6) 실행해서 나온값이 예를 들어 3이라면
$dice[3] 1증가시켜

입력회수만큼 다 동작하면
표 형태로 주사위 번호별 발생횟수를 출력해.
아래에는 구글차트의 라인차트를 이용해서 1~6까지 몇회씩
출현하는지 시각적으로 보여주.
dice.php파일을 만들어 줘.
```

**fake데이터 만들기**

```
fake.php파일을 만들고 싶어.
$name1="김,김,박,최,이,오,선우,독고";
이렇게 성씨들이 나열되있어.
같은방법으로 $name2는 이름의 가운데 글자 목록
$name3은 이름의 미지막글자를 적을거야.
$name1~$name3까지의 값을 50개씩 같은 방법으로 채워줘.
이때 사용되는 데이터는 조선시대 역사인물 이름에서 발췌해.

그런다음 dice만드는 것처럼
사용자로 부터 입력 횟수를 입력 받고, "생성하기"버튼을 클릭하면
$randname1$randname2$randnam3
과 같이 fake 이름 데이트를 생성하고 싶어.
또, 생년월일은 1500~1900년까지 임의의 날짜를 지정해
출신지는 서울, 경기, 충청, 전라, 경상, 제주 중에서 하나를  무작위로 뽑아.
최종 결과는 순서, 이름, 생년, 지역 순으로 표 형태로 정리해
```

**crawling**

```
https://www.snu.ac.kr/snunow/press?page=1
이 사이트를 크롤링해서 게시글의 제목을 가져와 출력하는 프로그램을 crawling.php 파일로 만들고 싶어.

page는 1페이지부터 10페이지까지만 순차적으로 가져올거야.

소스보기를 했을 때 다음과 같이 되어 있어.

         <tr>
            <td class="col-title new file">
              <a href="/snunow/press?md=v&bbsidx=179513">
                <span class="clip"><span class="txt">데이터사이언스대학원 김형신 교수팀, 인간 신경계 모사한 센서 중심 차세대 물리 AI 구조 개발</span></span>
                <span class="icon-new">새글</span>
                <span class="icon-file">첨부파일 있음</span>
              </a>
            </td>
            <td class="col-date">2026. 11. 16.</td>
          </tr>
          <tr>
            <td class="col-title new file">
              <a href="/snunow/press?md=v&bbsidx=179486">
                <span class="clip"><span class="txt">농생대, 2026년도 상록농업생명과학대상 등 시상식</span></span>
                <span class="icon-new">새글</span>
                <span class="icon-file">첨부파일 있음</span>
              </a>
            </td>
            <td class="col-date">2026. 11. 16.</td>
          </tr>

          ...

이중에서 

데이터사이언스대학원 김형신 교수팀, 인간 신경계 모사한 센서 중심 차세대 물리 AI 구조 개발

농생대, 2026년도 상록농업생명과학대상 등 시상식

이 두개가 제목이야.
실제 문서에서는 페이지당 10개씩 있는데, 이것은 너가 판단해.

각 페이지의 제목을 표 형태로 정리해 줘.

1페이지가 끝나면 2페이지, 3페이지 처럼 순차적으로 하는데
시스템에 부담을 줄이기 위해 5초마다 한번 요청해.
curl을 이용해서 처리해 줘.


```

C:\xampp\php\php.exe -n -d extension_dir="C:\xampp\php\ext" -d extension=curl -m


### 4일차 ###

## 4.1 로그 관리

```
다음과 같이 동작하는 log.php 파일을 만들어줘.
탭메뉴 형태로 3개를 만들거야.
탭 1: 표
탭 2: 차트(일)
탭 3: 차트(주간)

index.php?cmd=log&tab=1

만약 tab이 없으면 기본값은 1이야.
tab=1일 때의 동작

최근부터 역순으로 페이지당 30개씩 가져와서 표 형태로 출력
하단에 페이지네이션으로 구분하고 싶어.
만약 페이지가 너무많으면 페이지 출력하는 부분이 너무 많아지는 문제가 있어서 그룹핑을 하고 싶어.
한 그룹당 5개씩만 보고 싶어.
즉
  <맨앞> <이전> 11, 12, 13, 14, 15 <다음> <마지막>
와 같은 형태로 보여주고 싶어.
<맨앞>은 3그룹 이후에만 활성화
<이전>은 2그룹 이후에만 활성화
<다음>은 다음그룹이 존재할 때만
<마지막>은 총그룹수-현재그룹이 2이상일 때 활성화

표의 열은
idx, ip, id, work, time, flag, 비고
이중 flag는 예비영역인데, 접속한 ip의 국가 국기를 보여줄 예정이야.
비고란은 버튼 두개를 만들어서
ip 상세정보, 지도 보기 용도로 활용할 예정이ㅑ.
버튼 2개 각각 만들어줘.

tab = 2 일때의 동작
오늘 하루의 접속 컴퓨터수와 클릭수를 구글차트의 라인차트로 보여주고 싶어.

오늘 0시부터 24시까지 시간대별로 컴퓨터수(ip 수), 클릭수(로그수)를 그래프로 보이고 싶어.
그래프가 지속적으로 모니터링 되기 위해서 5초마다 새로고침해서 차트를 그려줘.
자바스크립트의 setTimeout()을 활용하면 돼.

tab = 3일때는
tab 2일때와 동작은 거의 같아.
오늘부터 6일전부터, 시간대별로 컴퓨터수, 클릭수를 라인차트로 그리고, 10초마다 새로고침해


```

https://www.daum.net/

**enum**

```c
    enum error_code {
        Trying = 100, Ringing = 180,
        OK = 200,
        BadRequest = 400,
        AuthError, Forbidden, NotFound, MethodNotAllowed, ..
    }
```

tElephoneNUMber : ENUM


**ip --> information**

IP 주소 정보 웹으로 얻어오기
http://ip-api.com


```
http://ip-api.com/json/1.2.3.4
와 같이 ip주소를 입력하면 JSON으로 가져오는 API가 있어.
다음과 같은 형태로 가져오고 있어.

{"status":"success","country":"Australia","countryCode":"AU","region":"QLD","regionName":"Queensland","city":"South Brisbane","zip":"4101","lat":-27.4767,"lon":153.017,"timezone":"Australia/Brisbane","isp":"Resource Quality Assurance","org":"Resource Quality Assurance","as":"","query":"1.2.3.4"}

이것을 프로그램으로 만들기 위해 ipinfo.php파일을 만들고 싶어.

상단에는 IP를 입력받고, "실행"버튼을 누르면 하단에
JSON으로 가져오는 프로그램 예제를 만들어줘.
출력을 보기 좋게 PRETTY_PRINT해서 보여줘.

```

**ipmap**

```
직전에 만든 ipinfo.php파일을 수정해서 ipmap.php을 만들고 싶어.
지도가 시작되기 전에 버튼을 하나 만들어.
버튼에는 "지도보기 (위도, 경도)"라고 표시.
버튼을 클릭하면
https://google.com/maps?q=경도,위도
이 창을 띄우고 싶은거야.
그런데 팝업으로 띄우지 말고 modal창으로 띄우고 싶어.
현재창의 가로, 세로의 90%를 차지하도록 모달창을 띄워.
```

**log + ip + map**

```
첨부한 log.php를 수정해서 log2.php 파일을 만들고 싶어.
tab = 1일때만 수정하면 돼.

버튼 두 개의 동작을 완성할거야.
첫번째 버튼은 ip주소를 이용해서, 
ipinfo.php 에서 동작한 것과 같이,
ip-api.com/json/IP 주소로 요청한 결과를 
PRETTY_PRINT 형태로 출력할거야.
출력할 곳은 Bootstrap5의 Offcanvas를 활용할거야.
방향은 왼쪽에 출력되고 싶어.

두번째 버튼은 지도보를 할 건데,
ipmap.php에서 동작한 것과 같은 원리로, 구글지도로 표시할거야.
출력할 곳은 Offcanvas의 위에서 아래로 내려오는 형태로 진행해. 그런데 전체 화면의 90%를 차지하도록 해 줘.
```

- [x] 국기로 로그 남기기

**struct의 이해**

struct my_struct {
    int a;      // 4B
    char b;     // 1B
    int c;      // 4B
    char d;     // 1B
};

typedef unsigned int uint32  ;
typedef unsigned short uint16  ;
typedef unsigned char uint8  ;

struct tcp_h {
    uint16 srcport;
    uint16 desport;

    uint32 seq;

    uint32 acnum;

    uint16 offset:4;
    uint16 rsv:6;
    uint16 syn:1;
    uint16 ack:1;
    uint16 fin:1;
};


**network log**
```
log 테이블에서 ip, time정보를 가져오고 싶어.
D3JS의 네트워크 다이그램을 이용해서 접속한 컴퓨터를 시각화하고 싶어.
즉, 노드와 링크 정보를 만들거야.
IP 대역별로 구분하고 싶어.
만약 1.2.3.4, 1.2.3.5가 접속했다면
1.2.3 노드가있고, 1.2.3.4와 1.2.3.5가 1.2.3노드에 연결되는 구조야.
이렇게 만들어진 접속 기록을 data.json 파일에 저장해줘.
만약에 data.json이 있는 경우에는, 이 파일을 지우고 다시 만들어져.

그런데, 이중에서 1.2.3 노드의 크기와 색상을 스케일링하고 싶어.

1회 ~ 30회 까지를 원의 지름 크기로 결정하고, 30이상은 모두 30픽셀의 크기로 고정시킬거야.
반대로 1회 ~ 20회까지는 색을 흰색->빨간색으로 노드의 색을 정하고, 20회 이상은 모두 빨간으로 처리해 줘.

네트워크 다이그램에서 1.2.3 네트워크가 1회인 것은 데이터에서 제외시켜줘.
마우스의 휠로 상하로 움직이면 확대 축소시켜줘.
오른쪽 마우스를 누르면 그래프 전체가 이동되도록 해 줘.
1.2.3 노드에 마우스를 올리면 여기에 접속한 컴퓨터 수와, 총 횟수를 함께 풍선도움말로 표시해.
최종 노드인 1.2.3.4에 마우스를 올리면, 총 몇회인지 출력하고(풍선도움말)고, 접속한 모든 시간을 나열해 줘.


```

**collapsible tree**

구글 검색: collapsible tree d3js

https://observablehq.com/@d3/collapsible-tree

```
비슷한 방법으로 collapsible tree를 d3js로 만들고 싶어.
서버 - 1 - 1.2 - 1.2.3 - 1.2.3.4 의 총 5단계로 구성할거야. 즉 네트워크 대역별로 세분해서 보고 싶어.
만약 1 - 1.2 - 1.2.3 - 1.2.3.4 네트워크별로
30, 15, 10, 4 번 접속한 기록이 있다면,
1(30) - 1.2(15) - 1.2.3(10) - 1.2.3.4(4)
와 같이 컴퓨터 수를 표시해 줘.
색깔별로 1~ 50회까지를 흰색~빨간색으로 표시하고, 
50회 이상은 빨간색으로 표시해.
일반적인 collapsible 와 같이
하위 노드가 있는 경우는 앞의 색상 정하는 원칙에 의해
원의 색을 채워주거나, 비워서 하위노드 여부를 쉽게 판단할 수 있게 해 줘.
tree.php 파일을 이렇게 동작하도록 만들어 줘.
```

**black list**

```
블랙리스트 ip 주소를 관리하기 위한 black을 스키마로 만들고 싶어.
idx : integer, auto_increment, primary key,
ip : ip address
time : datetime,
rejects int default '0'

이때 rejects는 목록에 추가된 후, 차단되는 회수를 추가할 목적이야.
black 테이블의 스키마를 제시해

```

**result**

```sql
CREATE TABLE black (
    idx INT NOT NULL AUTO_INCREMENT,
    ip VARCHAR(45) NOT NULL,
    time DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    rejects INT NOT NULL DEFAULT 0,

    PRIMARY KEY (idx),
    UNIQUE KEY uq_black_ip (ip)
) ENGINE=InnoDB
  DEFAULT CHARSET=utf8mb4
  COLLATE=utf8mb4_unicode_ci;
```

게시판 만들기 (블랙리스트)

```
첨부한 board.php를 수정해서 board2.php를 만들고 싶어.
이중에서 게시판 보기 기능만 바꾸면 돼.
관리자로 접속한 경우, 게시글의 하단에 버튼 하나를 추가해야 해.
<블랙리스트>
이 버튼을 누르면 confirm('블랙리스트에 추가하시겠습니까?')라고 물어줘.

이때, 조금 전에 만든 black 테이블에 추가해줘.
```


# 5일 #

## 5.1 black 차단

```sql
INSERT INTO black (ip, time, rejects)
VALUES
    ('11.25.3.57', NOW(), 0),
    ('11.25.3.66', NOW(), 0),
    ('11.25.1.17', NOW(), 0),
    ('13.22.3.56', NOW(), 0),
    ('13.25.3.49', NOW(), 0),
    ('11.23.2.77', NOW(), 0),
    ('11.24.1.32', NOW(), 0),
    ('11.22.2.14', NOW(), 0),
    ('12.22.3.14', NOW(), 0)
ON DUPLICATE KEY UPDATE ip = VALUES(ip);
```

**web ftp**

```
ftp.php 파일을 만들고 싶어.
윈도우 탐색기처럼 왼쪽은 디렉토리 목록이 나오고,
오른쪽은 파일 목록이 나오게 하고 싶어.
가능하면 시각적으로 보기 편하게 표의 한 셀처럼
세로형태로 나열하고 싶어.
디렉토리 목록에는
.
..
data
img
이런 형태로 배치될텐데, 
맨 위에는 처음으로 가기 버튼을 만들고 싶어.
각 디렉토리를 클릭하면 해당하는 디렉토리로 이동하고 싶어.

오른쪽은 파일 목록을 보여주는데, 
예를 들어 index.php, ftp.php, board.php 등이 있어.
디렉토리목록과 파일목록은 오름차순으로 정렬해서 보여줘.
파일이름을 클릭하면
offcanvas로 왼쪽에서 나와도록하고, 그 내용을 textarea에 편집할 수 있도록 해줘.
만약 jpg와 같이 이미지파일인 경우, 이미지를 보여줘.

offcanvas의 화면 구성은 편집가능한 php, txt 등의 파일이라면, 
<textarea>파일의 내용 </textarea>
<input type="text" name="filename"><저장버튼>

filename이 입력된후 버튼을 클릭하면 입력된 값으로 새로 생성해줘. 만약 현재 보고 있는 파일이 
a.php인데, filename이 b.php파일이면
현재 내용을 b.php로 저장하는 거야.

또, a.php인데, filename도 a.php이면
기존에 있는 a.php파일을 지우고, a.php라는 이름으로
내용을 저장해 줘.
```

```
<textarea rows="10">으로 바꿔 항상 일정 높이가 되도록해야하고,
offcanvas의 <textarea>밑에 파일 이름 입력하고 저장하는 기능이 만들어지지 않았어.
이를 반영해 줘.
```

```php
<?
    include "../db.php";
    $conn = connectDB();
?>
```

**도구**

```
SAST: Static Application Security Testing
    코드 분석
    CodeSonar : C, C++
    SonarQube, 
DAST : Dynamic AST
    OWASP ZAP
main()
{
    if(test("hello")<0)
    {

        // error
    }
}
int test(*ptr)
{
    char errrorMsg[100];

    if(!ptr)
    {
        // errror
        errorMsg = "파라미터 에러";
        goto ErrorControl;
        return -1;
    }


    ... // error
    errorMsg = "연산 에러";
    goto ErrorControl;

    return -1;



    // error
    return -1;

    strcpy(ptr, buf);

ErrorControl:
    log(errroMsg);
    return -1;
}   


OWASP Dependency-Check

```

**Performance**

```
http://localhost/data/
이런식으로 접속하면 파일의 링크가 보이는 문제가 있어.
이를 해결하기 위한 방법으로는 .htaccess를 최상위 디렉토리 넣어 설정하는 방법이 있고,
나머지 하나는 아파치 설정을 바꾸는 방법이 있어.
첫번째 방법을 위한 .htaccess 파일을 만들어줘.
아파치 설정으로 해결하는 방법도 추가적으로 설명해 줘.

```

**.htaccess**

최상위 디렉토리에  

Options -Indexes


**backup**

mysql -u secure secure -p

mysqldump -u secure secure -p >secure-2026-11-20-fin.db.sql

**clean code**

```c
void test()
{
    int     age_i; // iAge
    float   level; // fLevel
    double  score; // dScore
    // mAge

    typedef struct tcp_t 
    {

    }

    age = age + 1;
}
```

**thread**

```
    slow.php 파일을 하나 만들거야.
    index.php?cmd=slow&com=1&count=3
    이런 형태로 호출할거야.
    1초동안 sleep한 후,
    com = 1, count = 3이라 출력하는 코드야.
    또, 화면에 측정된 시간을 초 단위와 ms 단위로도 출력해줘.
    

    attack.php 파일을 만들거야.
    상단에 두개의 입력창이 있어.
    하나는 컴퓨터갯수를 1~50개까지 결정할 수 있고, 기본값은 10개야.
    하나는 실행횟수를 1~30회까지 결정할 수 있고, 기본값은 5회야.
    그 옆에 "실행" 버튼을 클릭하면 동작하는 코드야.
    이 파일은 공격하는 PC개수와 공격회수를 입력받아서
    DDoS 흉내만 내려고 하는거야.
    자바스크립트로 fetch()를 반복적으로 수행해서
    시스템에 미치는 영향을 보고 싶어.
    index.php?cmd=sleep&com=컴퓨터번호&count=실행회차

    이렇게해서 DDoS 공격이 성능에 미치는 영향을 측정하는 프로그램을 만들어줘.
```

**resource**

```
현재 내 시스템은 PHP로 동작하는데,
windows 11에서 xampp환경이야.
그런데 CPU, Memory 사용률을 확인하는 resource.php 파일을 만들고 싶어.
윈도우이기 때문에 필요한 경우에는 파워쉘을 이용해서 수행하고 싶어.
이 파일은 index.php?cmd=resource 이렇게 접속하는데
3초마다 새로고침해서 새로운 CPU, Memory 점유율을 확인하고 싶어.
```


**예제**
```
    int *ptr = null;
    int age =3;

    ptr = &age;

    메모리 크기의 한계
```
