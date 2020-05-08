### list
- list [1, 2, 3, 4]
- 함수
    - append, pop, insert, index('', 1), count('')

### set
- set {1, 2, 3, 4}
- 함수
    - union, intersection(교집합)

### tuple
- tuple (10, 20)
- 함수
    - 

### dict(사전)
- dict(one=1, two=2, three=3)
- a = {one:1, two:2, three:3}
    - a[one]
    - a[four] = 4
- 문법
    - del a[one]
    - a.clear()
    - a.items()
    
~~~ python
    for k, v in a.items():
        print(k, v)

    for k in a.keys():
        print(k)        

    for v in a.values():
        print(v)                
~~~