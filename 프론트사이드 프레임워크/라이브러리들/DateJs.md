#### Date.js
~~~ js
// What date is next thursday?
Date.today().next().thursday();
 
// Add 3 days to Today
Date.today().add(3).days();
 
// Is today Friday?
Date.today().is().friday();
 
// Number fun
(3).days().ago();
 
// 6 months from now
var n = 6;
n.months().fromNow();
 
// Set to 8:30 AM on the 15th day of the month
Date.today().set({ day: 15, hour: 8, minute: 30 });
 
// Convert text into Date
Date.parse('today');
Date.parse('t + 5 d'); // today + 5 days
Date.parse('next thursday');
Date.parse('February 20th 1973');
Date.parse('Thu, 1 July 2004 22:30:00'); 

※ Date.today()는 오늘 날짜에 시간은 00:00:00으로 초기화 되어 리턴된다.
즉 new Date().clearTime()과 동일하다

var toDate = new Date();
var measur_dt = toDate.toString("yyyy-MM-dd HH:mm:ss");
alert(measur_dt);
~~~