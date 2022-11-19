
## CSV파일을 열의 내용에 따라 정렬(sort, 리다이렉트)

- csv파일 자체는 일반 텍스트 파일이므로 문자열 조작 명령어로 간단히 가공할 수 있다

- 작업순서
    - 불필요한 열을 삭제하기
    - 줄을 재고수 크기로 재정렬
    - 결과를 파일로 출력하기


- cut은 일부 열만 추출하는 것 뿐만아니라 일부 열을 제거하는 것도 가능하다
- csv 파일은 구분자 콤마를 써서 줄의 내용을 필드 단위로 나눈 텍스트 파일

```
$ itmes.csv cut -d "," -f 3
$ items.csv cut -d "," -f 1,2,3,4
$ items.csv cut -d "," -f 1-3
```

- sort 명령어도 cut처럼 특정 구분자로 나누는 기능이 있다
    - --field-seperator(-t) 옵션으로 구분자를 지정하고
    - --key(-k) 옵션으로 열 번호를 지정하면 그 열 내용으로 재정렬한다 
    
    
- cut --delimiter "," -fields 3
- cut  -d         "," -f     3
    
    
- sort --field-seperator "," --key 3
- sort  -t               ","  -k   3

```
# sort는 단순정렬한다. 예를 들어 아래와 같은 경우 첫 글자로 재배치 한 다음 두번째 글자로 재배치 한다 
1, ubuntu
2, Debian
11, Fedora
10, Red Hat

#결과
1, ubuntu
10, Red Hat
11, Fedora
2, Debian

# 따라서 --number(-n) 옵션 사용한다
# -n 옵션을 사용하면 숫자로 해석해서 값의 크기로 재정렬한다 

$ cat items.csv |cut -d "," -f 1-3"| sort -t "," -k 3 -n |less



# uniq -c 결과는 숫자가 오른쪽 정렬이다. 따라서 아래 두 과정을 거쳐서 정렬된다 

# 스페이스는 문자코드표에서 1보다 위에 온다
 1, ubuntu
 2, Debian
11, Fedora
10, Red Hat

# 두번째 글자로 재배치
 1, ubuntu
 2, Debian
10, Red Hat
11, Fedora


# 스페이스로 칸을 채워서 오른쪽으로 줄맞춤한 문자열은 단순정렬해도 기대한 것과 다른 결과가 나올 수 있다 
# 따라서 --igonore-leading-blanks(-b) 옵션을 사용하면 오른쪽줄맞춤을 위해서 넣은 스페이스를 무시하고 문자열을 정렬할 수 있다 

$ cat items.csv |cut -d "," -f 1-3"| sort -t "," -k 3 -n | -b |less

```


<hr>

- 리다이렉트
    - 명령어 실행결과를 저장하는 본 테크닉
    - | 대신 > 를 사용하면 보통은 파이프라인으로 넘어가는 것과 같은 내용이 텍스트 파일로 출력된다
    


```

# >를 사용하는 경우 리다이렉트는 이미 파일이 있으면 지우고 새로운 파일을 만든다
$ cat items.csv |cut -d "," -f 1-3"| sort -t "," -k 3 -n > ./items-sorted.csv

#>>를 사용하는 경우 기존 파일에 추가한다 

$ echo "12345" >> ./items-sorted.csv


```

### Reference
  - [만화로 배우는 리눅스 시스템 관리](http://www.yes24.com/Product/Goods/32402055?Acode=101)
