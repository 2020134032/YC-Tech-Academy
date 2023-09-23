# 3주차 RDBMS
## 1~3
정리자 : 정준

- unique key, primary key
- foreign key
<hr>

- primary and unique key does not allow duplicate values

- primary key는 테이블에 하나, unique는 여러 개 가능   
- unique key는 NULL도 받음 (primary는 안 받음)   
- 다른 테이블에서 foreign 키로 사용 가능함   
  
```sql
CREATE TABLE CUSTOMERS (
   ID INT NOT NULL UNIQUE KEY,
   NAME VARCHAR(20) NOT NULL,
);

-- unique key 설정 예시
```

```sql
ALTER TABLE table_name ADD CONSTRAINT unique_key_name UNIQUE (column_name);

-- unique key on existing column
```

```sql
ALTER TABLE table_name DROP CONSTRAINT unique_key_name;

-- unique key drop
```

유니크 키 - 중복값 방지에 초점

프라이머리 키 - 테이블 레코드 구분에 초점

## foreign key

- 다른 테이블의 primary키값을 가짐   
![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/2758bb9f-476c-4510-b346-22c2eeb642ae)
- 중복 제거 (remove redundancy)
- normalization (정규화)
- 유효하지 않은 값 방지

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
    CONSTRAINT fk_name 
	FOREIGN KEY (column_name) 
	REFERENCES referenced_table(referenced_column)
);
```

- foreign 키의 reference로 등록되어 있는 컬럼 테이블은 마음대로 drop할 수 없음
```sql
ALTER TABLE table_name DROP FOREIGN KEY (constraint symbol);
-- dropping foreign constraint

ALTER TABLE TABLE2 
ADD CONSTRAINT[symbol] 
FOREIGN KEY(column_name) 
REFERENCES TABLE1(column_name);
-- adding constraint
```

![image](https://github.com/2020134032/YC-Tech-Academy/assets/128214994/e06a5541-fb4d-49d5-8169-7868399c9ab4)


