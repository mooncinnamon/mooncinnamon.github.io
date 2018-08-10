### 데이터가 없다면 insert 있다면 update 할 수 있을까?

가끔 Query문을 작성하다 보면 생기는 부분 중 의문이다.

"나는 Insert 하거나 Update 하고 싶은데... 매번 Select문으로 검사를 해 줘야 하나?"

항상 코드 상에서 Select 후 분기를 만들어서 insert나 update를 해 주었는데 궁금하기도 해서 검색을 해 보았다.



[Stackoverflow - Insert if no exists else update?](https://stackoverflow.com/questions/3634984/insert-if-not-exists-else-update)



스택 오버플로우에서 나랑 같은  생각을 한 사람은 역시 존재했다.

```sql lite
INSERT OR REPLACE
```

를 사용하면 삽입하거나 수정하거나 할 수 있다고 한다.