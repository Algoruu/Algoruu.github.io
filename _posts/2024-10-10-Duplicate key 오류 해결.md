---
layout: post
title:  "Duplicate key 오류 해결"
excerpt: "Duplicate key 오류 해결"
category: mysql
tags: [mysql]
date: '2024-10-10 15:00:00 +09:00'
last_modified_at: '2024-10-10'
---
# Duplicate key 오류 해결

## 🌊 errno: 121 "Duplicate key on write or update”

<span style="color:lightseagreen">💫 **제약조건 이름 정해주기**</span><br>

외래키 제약조건의 이름때문에 errno: 121 "Duplicate key on write or update”이 발생한 것!<br>
즉 외래키 제약조건이름이 다른 테이블의 외래키 제약조건이름과 겹치기때문!<br>

[**FK 제약조건 이름 짓기**]<br>
fk_기준 테이블명_참조테이블명_참조키<br>
**cartItems.user_id > users.id** : fk_cartItems_users_id<br>
**likes_user_id > users.id** : fk_likes_users_id<br>

<img src="https://github.com/Algoruu/Algoruu.github.io/blob/main/_programmers/img01/image-359.png?raw=true">
- 하지만 또 오류가 발생함!<br>
ERROR 1061: Duplicate key name 'book_id_idx'<br><br/>

## 🌊 ERROR 1061: Duplicate key name 'book_id_idx'
<span style="color:lightseagreen">💫 **인덱스 이름 고치기**</span><br>

ERROR 1061: Duplicate key name 'book_id_idx'가 에러가 발생한 이유는 자동으로
sql에서 관리하기 쉽게 인덱스를 추가해주는데, 인덱스 이름이 변경되지 않은 것!<br>

**index** : 데이터베이스 내에서 일종의 목차를 생성한다고 생각하면 됨.<br>

<img src="https://github.com/Algoruu/Algoruu.github.io/blob/main/_programmers/img01/image-360.png?raw=true">
- 이렇게 index 이름도 수정하면 잘 작동함!!<br><br>

따라서 Duplicate key 오류는 이름을 겹치지 않게, 일정한 규칙을 따라서 지을 것이 핵심임!<br> 
