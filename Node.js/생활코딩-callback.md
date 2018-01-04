# 생활코딩 Node.js & Express - callback

- 예제 sort()
```bash
$ node
> a = [3,1,2]; a.sort(); console.log(a);
[ 1, 2, 3 ]

> a = [3,1,2]; function b(val1,val2){return val2-val1};  a.sort(b); console.log(a);
[ 3, 2, 1 ]

> a = [3,1,2]; function b(val1,val2){return val1-val2};  a.sort(b); console.log(a);
[ 1, 2, 3 ]

> a = [3,1,2]; a.sort((val1,val2)=>{val2-val1}); console.log(a);
[ 3, 1, 2 ]
# 익명함수
```