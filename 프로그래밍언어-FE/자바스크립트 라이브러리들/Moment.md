#### Momont.js
- 날짜를 손쉽게 다룰수 있는 moment.js

~~~ js
// 날짜 지정하기
moment('2019-12-10', 'YYYY-MM-DD');

// Format 이용하기
// format()을 하면 moment객체에서 string으로 반환을 합니다.
moment().format('YYYY-MM-DD'); // 년도-월-일
moment().format('hh:mm:ss'); // 시:분:초
moment().format('dddd'); // Tuesday

// 날짜 더하고 빼기
moment().add(1,'days') // 하루 더하기
moment().subtract(1,'days') // 하루 빼기
moment().add(1,'months') // 한달 더하기
moment().subtract(1,'year') // 1년 빼기

const nowDate = moment('2019-12-10');
const nextDate = nowDate.clone().add(1,'days'); // 2019-12-11
const prevDate = nowDate.clone().subtract(4,'days'); // 2019-12-06
console.log(nowDate); // 2019-12-10

// isBefore, isAfter
// 두값이 이전 혹은 이후인지 비교합니다.

// isBefore 첫번째 값이 두번째 값보다 이전인가?
moment('2010-10-20').isBefore('2010-10-21'); // true 
// isAfter 첫번째 값이 두번째 값보다 이후인가?
moment('2010-10-21').isAfter('2010-10-20'); // true
moment('2010-10-20').isBefore('2010-12-31', 'year'); // false
moment('2010-10-20').isBefore('2011-01-01', 'year'); // true

// isSame
// 두날짜가 같은지 비교합니다.
moment('2010-10-20').isSame('2010-10-20'); // true

// isSameOrAfter, isSameOrBefore
// 두값이 같거나 이전이거나, 두값이 같거나 이후인지 비교합니다.
moment('2010-10-20').isSameOrBefore('2009-12-31', 'year'); // false
moment('2010-10-20').isSameOrBefore('2010-12-31', 'year'); // true
moment('2010-10-20').isSameOrBefore('2011-01-01', 'year'); // true

// isBetween
// 두값의 사이값이 맞는지 비교합니다.
moment('2010-10-20').isBetween('2010-10-19', '2010-10-25'); // true

~~~