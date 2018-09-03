## isAlphaNumeric

#### 영어 문자열이 주어졌을때 숫자, 대문자, 소문자 이외의 단어가 들어갔는지 확인하는 알고리즘

아스키코드를 이용한 알고리즘
```javascript
function isAlphaNumeric(str) {
    var code;

    for(var i = 0, len = str.length; i < len; i++) {
        code = str.charCodeAt(i);
        if(!(code > 47 && code < 58) &&
           !(code > 64 && code < 91) &&
           !(code > 96 && code < 123)) {
            return false;
        }
    }
    return true;
}
```

정규표현식을 이용한 알고리즘
```javascript
function isAlphaNumeric(str) {
    return /^[a-zA-Z0-9]+$/.test(str);
}
```
성능상으로는 아스키코드를 이용한 알고리즘이 정규표현식을 이용한 알고리즘보다 빠르다고 한다.