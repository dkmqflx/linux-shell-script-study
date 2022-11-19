
## Ch23. 같은 처리 반복해서 실행(for)

- for 반복문
    - 같은 처리를 조금씩 인수(처리 대상 파일명 등)를 바꾸어 가면서 반복실행하는 구문

```
for filename in redmine.log kintal.log download.log
do
    ./create-report.sh $filename
done
    
# for ~ in 은 줄바꿈을 쓰지 않는다. 줄바꿈을 할 경우 \ 사용
for filename in redmine.log \
                kintal.log \
                download.log
do
    ./create-report.sh $filename
done
```

- for 반복문 안에서 명령어 치환을 사용할 수 있다
    - /var/log/apache2 위치에 있는 확장자가 .log인 파일
    - 단, error.log는 제외

```
# for filename in redmine.log kintal.log download.log 이 부분을 아래와 같이 대체
for filename in cd /var/log; ls *.log | grep -v error.log
```

- for 반복문은 줄바꿈 대신에 ;(세미콜론)을 쓰면 한줄로 만들어서 일반 명령어처럼 실행가능하다

```
for file in data log script; do echo $file; done
do
    ./create-report.sh $filename
done
```

## Reference

  - [만화로 배우는 리눅스 시스템 관리](http://www.yes24.com/Product/Goods/32402055?Acode=101)
