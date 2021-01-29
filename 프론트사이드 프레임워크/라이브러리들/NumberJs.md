### Number.js
- 통화 표시, 천 단위 콤마 등 숫자 형식 지정할 때 유용한 라이브러리
~~~ js
numeral( 1000 ).format( '0,0' ); // 1,000
numeral( 1000 ).format( '0.00' ); // 1000.00
numeral( 1000 ).format( '₩0,0' ); // ₩1,000
~~~