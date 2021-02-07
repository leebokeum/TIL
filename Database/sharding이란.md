### sharding이란?
- 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법을 의미한다.
- application level에서도 가능하지만 database level에서도 가능하다.
- Horizontal Partitioning이라고 볼 수 있다.

### 샤딩(Sharding)에 필요한 원리
- 분산된 Database에서 Data를 어떻게 Read할 것인가?
- 분산된 Database에 Data를 어떻게 잘 분산시켜서 저장할 것인가?
- 분산이 잘 되지 않고, 한 쪽으로 Data가 몰리게 되면 자연스럽게 Hotspot이 되어 성능이 느려지게 된다.
- 그렇기 때문에 균일하게 분산하는 것이 중요한 목표이다.

### 샤딩(Sharding) 방법
- Shard Key를 어떻게 정의하느냐에 따라 데이터를 효율적으로 분산시키는 것이 결정


### 샤딩(Sharding)이 꼭 좋은것만은 아니다.
- 샤딩(Sharding)을 적용한다는것은?
    - 프로그래밍, 운영적인 복잡도는 더 높아지는 단점이 있습니다.
- 가능하면 Sharding을 피하거나 지연시킬 수 있는 방법을 찾는 것이 우선되어야 합니다.
  - Scale-in
      - Hardware Spec이 더 좋은 컴퓨터를 사용합니다.
  - Read 부하가 크다면?
      - Cache나 Database의 Replication을 적용하는 것도 하나의 방법입니다.
  - Table의 일부 컬럼만 자주 사용한다면?
    - Vertically Partition도 하나의 방법입니다.
    - Data를 Hot, Warm, Cold Data로 분리하는 것입니다. Link


### 참조
https://nesoy.github.io/articles/2018-05/Database-Shard