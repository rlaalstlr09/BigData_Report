201945069 김민식 
빅데이터 레포트
1. 정규표현식에 관한 설명
2. 가비지 컬렉션에 관한 설명

# 1. 정규표현식 (regex)



## 정규표현식이란? : 
            특정 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식언어

            많은 텍스트 편집기와 프로그래밍 언어에서 문자열의 검색과 치환을 위해 지원
            
            파이썬에서는 정규표현식 사용을 위해 re 모듈을 사용해야 한다.



## 파이썬에서의 문법 :

   #### - 리터럴 문자 : 문자의 패턴을 나타낸다.

            ex) a : a

                a-z : a~z까지 모든 소문자 알파벳 

                0-9 : 모든 숫자

                파이썬에서는 한글을 지원하지 않기 때문에 한글 사용을 위해서는 유니코드로 지정해야 한다.


#### - 메타문자 : 원래 그 문자가 가진 뜻이 아닌 특별한 용도로 사용하는 문자. 정규표현식에서는 메타문자를 이용해 동작한다.

            종류 : '.'(마침표) : 임의의 한 문자와 일치

                  '*' : 앞 문자 패턴이 0개 이상 일치

                  '+' : 앞 문자 패턴이 1개 이상 일치

                  '?' : 앞 문자가 없거나 하나 있음

                  '[]' : 문자클래스

                  '\d' : 숫자

                  '\D' : 숫자가 아닌 것

                  '\w' : 문자 , 숫자 , _

                  '\W' : 문자 , 숫자 , _ 가 아닌 것

                  '\s' : 공백 문자

                  '\S' : 공백 문자가 아닌 것

                  '^' : 문자열의 시작

                  '$' : 문자열의 종료
   

  #### - 수량자 : 패턴이 반복하는 횟수를 나타낸다.

            종류 : {n} : n번 반복할 때 일치

                  {n,} : n번 이상 반복할 때 일치

                  {n,m} : n번에서 m번 반복할 때 일치


   #### - re 모듈에서 패턴 객체를 사용한 문자열 검색 method

            종류 : match() : 문자열의 처음부터 정규식과 매치되는지 확인

                  search() : 문자열 전체를 검색하여 정규식과 매치되는지 확인

                 findall() : 정규식과 매치되는 모든 문자열을 리스트로 돌려줌

                 finditer() : 정규식과 매치되는 모든 문자열을 반복 가능한 객체로 돌려줌


   #### - match(), search()를 수행한 결과로 돌려준 match 객체가 사용하는 함수

            종류 : group() : 매치된 문자열을 돌려줌

                  start() : 매치된 문자열의 시작 위치를 돌려줌

                  end() : 매치된 문자열의 끝 위치를 돌려줌

                  span() : 매치된 문자열의 (시작, 끝)에 해당하는 튜플을 돌려줌



   ## Regex.ipynb : 
            간단한 정규표현식 예제

            text 문자열에 있는 이메일과 한글을 찾는 규칙을 정의하고 대표적인 findall, match, search 함수를 사용해보는 예제




# 2. 가비지 컬렉션 (GC)



## 필요 : 
            가비지 컬렉션(Garbage Collection)은 프로그래밍 언어에서 자동으로 메모리 관리를 수행하는 메커니즘이다.

            가비지 컬렉션은 사용되지 않거나 더 이상 참조되지 않는 객체의 메모리를 해제하여 메모리 누수를 방지하고 리소스 사용을 최적화한다.

            가비지 컬렉션은 파이썬같은 동적 타입 언어에서는 자동으로 활성화되어 객체의 수명 주기를 추적하고 메모리를 해체하여 따로 명시해줄 필요가 없지만 따로 명시해주기 위해서는 gc 모듈을 사용한다.



## 사용하지 않으면 : 
            가비지 컬렉션을 사용하지 않으면 메모리 관리는 프로그래머가 책임져야 한다.

            메모리를 직접 해제하지 않거나 적절하게 관리하지 않으면 메모리 누수가 발생하여 메모리 소비 증가, 성능 저하, 메모리 부족으로 프로그램 충돌 등의 문제가 생길 수 있다.

            가비지 컬렉션을 사용함으로써 메모리 관리를 자동화 하여 메모리 누수를 신경쓰지 않고 코드 작성에 집중할 수 있게 된다.



## 파이썬에서의 동작 방식 :

   #### mark and sweep 알고리즘 : 
                        가장 일반적인 GC 알고리즘

                        마킹과 스윕 두 단계로 구성

                        마킹 당계에서 GC는 root object (전역변수, 스택 프레임 등) 의 집합에서 시작하여 도달 가능한 모든 오브젝트 마킹

                        스윕 단계에서 GC는 마킹되지 않은 오브젝트가 사용중인 메모리를 식별, 회수

                        회수된 메모리는 이후 메모리 할당에 사용



   #### 레퍼런스 카운팅 :
            파이썬의 각 오브젝트는 새로운 래퍼런스가 생성되면 레퍼런스 카운트 증가, 레퍼런스 범위를 벗어나거나 삭제되면 카운트 감소

            오브젝트의 레퍼런스 카운트가 0이 되면, 즉 더 이상 해당 오브젝트를 가리키는 레퍼런스가 없게 되면 해당 오브젝트가 사용중인 메모리 회수



## 제대로 동작하려면 :
            GC가 제대로 동작하기 위해서는 오브젝트의 레퍼런스를 관리하고, 오브젝트들 사이에 순환 참조가 발생하지 않도록 해야하며 대용량 데이터 구조를 관리해야한다.

            순환참조는 오브젝트들이 서로 참조하여 사이클을 형성하는 경우로 래퍼런스 카운트가 0이 되지 않아 가비지 컬렉션을 방해하게 된다.

            순환 참조를 피하기 위해서는 오브젝트들이 서로 무한히 참조하는 데이터 구조를 생성하지 않도록 해야하는데 적절한 경우 래퍼런스를 'None' 으로 설정하거나 'weakref' 모듈에서 제공하는 약한 레퍼런스를 사용하여 해결할 수 있다.

            대용량 데이터 구조 관리의 경우 대량의 메모리를 소비하기 때문에 불필요한 리소스를 직접 해제하거나 제너레이터, 이터레이터와 같은 효율적인 메모리 관리를 제공하는 데이터 구조를 사용하여 해결할 수 있다.



## gc 모듈 문법 : 
            gc.disable() : 파이썬에서 자동으로 활성화되는 GC를 비활성화한다. 일반적인 경우 권장하지 않는다.

            gc.collect() : 가비지컬렉션을 명시적으로 수행하도록 지시한다.

                           함수를 호출하면 가비지컬렉터는 메모리를 검사하여 가비지 객체를 탐지하고 해제한다.

                           일반적으로 레퍼런스 카운트가 3 이상 (기본 2, 참조횟수에 따라 값 증가) 일 경우 GC는 자동으로 객체를 해제하지 않기 때문에 순환 참조의 경우 gc.collect() 함수를 통해 명시적으로 메모리를 해제할 수 있다.

            gc.enable() : 비활성화 된 GC를 다시 활성화 시킨다.

            gc.get_referrers() : ()에 있는 객체를 참조하는 모든 객체 및 구조체를 반환

                                 참조상태를 알 수 있기 때문에 순환 참조등의 문제를 식별하고 수정, 참조 해제 할 때 용할 수 있다.



## GC.ipynb : 
            파이썬에서는 자동으로 GC가 작동되지만 그렇지 않은 경우를 테스트해보는 예제







