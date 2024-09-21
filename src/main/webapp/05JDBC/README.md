## in system 계정,
```
select tablespace_name, status, contents FROM dba_tablespaces;

SELECT tablespace_name, sum(bytes), max(bytes) FROM dba_free_space
 GROUP BY tablespace_name;
 
select username, default_tablespace FROM dba_users
 WHERE username IN upper('musthave');
 
ALTER USER musthave quota 5m ON users;
```

## in musthave 계정,
```
CREATE TABLE MEMBER
(
	id varchar2(10) NOT NULL,
	pass varchar2(10) NOT NULL,
	name varchar2(30) NOT NULL,
	regidate DATE DEFAULT sysdate NOT NULL,
	PRIMARY key(id)
);


CREATE TABLE board
(
	num NUMBER PRIMARY KEY,
	title varchar2(200) NOT NULL,
	content varchar2(2000) NOT NULL,
	id varchar2(10) NOT NULL,
	postdate DATE DEFAULT sysdate NOT NULL,
	visitcount number(6)
);

ALTER TABLE BOARD ADD CONSTRAINT board_mem_fk FOREIGN key(id) REFERENCES member(id);

CREATE SEQUENCE seq_board_num
	INCREMENT BY 1
	START WITH 1
	MINVALUE 1
	nomaxvalue
	nocycle
	nocache;
	

INSERT INTO member(id, pass, name) VALUES ('musthave', '1234', '머스트해브');
INSERT INTO board(num, title, content, id, postdate, visitcount)
VALUES (seq_board_num.nextval, '제목1입니다', '내용1입니다', 'musthave', sysdate, 0)
;
COMMIT;
```