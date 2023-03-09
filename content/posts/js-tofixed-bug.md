---
title: js中toFixed的bug
date: 2023-03-09
author: 夏明
---

今天在开发过程中发现了js的`toFixed`方法在四舍五入的时候有精度问题...

按道理`console.log((0.15).toFixed(1))`控制台应该输出 0.2 的，可是却是 0.1！

## 解决办法

重写Number原型上的toFixed 方法

```javascript
Number.prototype.toFixed = function (decimal) {
  let number = this
  decimal = decimal || 0;
  var s = String(number);
  var decimalIndex = s.indexOf('.');
  if (decimalIndex < 0) {
    var fraction = '';
    for (var i = 0; i < decimal; i++) {
      fraction += '0';
    }
    return s + '.' + fraction;
  }
  var numDigits = s.length - 1 - decimalIndex;
  if (numDigits <= decimal) {
    var fraction = '';
    for (var i = 0; i < decimal - numDigits; i++) {
      fraction += '0';
    }
    return s + fraction;
  }
  var digits = s.split('');
  var pos = decimalIndex + decimal;
  var roundDigit = digits[pos + 1];
  if (roundDigit > 4) {
    //跳过小数点
    if (pos == decimalIndex) {
      --pos;
    }
    digits[pos] = Number(digits[pos] || 0) + 1;
    //循环进位
    while (digits[pos] == 10 && pos !== 0) {
      digits[pos] = 0;
      --pos;
      if (pos == decimalIndex) {
        --pos;
      }
      digits[pos] = Number(digits[pos] || 0) + 1;
    }
  }
  //避免包含末尾的.符号
  if (decimal == 0) {
    decimal--;
  }
  return digits.slice(0, decimalIndex + decimal + 1).join('');
}
```



