# postgreSQL

PostgreSQL은 오픈소스 데이터베이스 중 가장 진보되고 안정적인 데이터베이스이며 ANSI/ISO 규격의 SQL을 지원하며,

Ingres(INteractive Graphics REtrieval System)에 뿌리를 두고 있다

초기 개발 단계부터 완벽한 ACID와 MVCC를 지원하는 아키텍쳐로 설계된 PostgreSQL은 대용량의 복잡한 트랜잭션 처리를

위한 RDBMS이다.

 - ACID(Transaction이 안전하게 수행된다는 것을 보장하기 위한 성질을 가리키는 약어)
  1) Atomicity : 원자성은 Transaction과 관련된 작업들이 부분적으로 실행되다가 중단되지 않는 것을 보장하는 능력이다. 원자성은 중간 단계까지 실행되다가 실패하는 일이 없도록 하는 것이다.
  2) Consistency : 일관성은 Transaction이 실행을 성공적으로 완료하면 언제나 일관성있는 DB 상태로 유지하는 것을 의미한다. 무결성 제약에 위반하는 Transaction은 중단된다.
  3) Isolation : 고립성은 Transaction을 수행 시 다른 Transaction의 연산 작업이 끼어들지 못하도록 보장하는 것을 의미한다. 이는 Transaction 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미한다. 또한 고립성은 Transaction 실행 내역이 연속적이어야함을 의미하고, 유연성있는 제약조건이다.
  4) Durability : 지속성은 성공적으로 수행된 Transaction은 영원이 반영되어야 함을 의미한다. System 문제나 DB 일관성 체크 등을 하더라도 유지되어야 하고, 모든 Transaction은 로그로 남긴 채로 Rollback도 가능하다. 
                  Transaction은 로그에 모든 것이 저장된 후에만 Commit 상태로 간주한다.

 - MVCC(Multi Version Cuncurrency Control): 쓰기와 읽기가 서로 블로킹하지 않아, 동일한 데이터에 접근했을 때의 동시성을 높이는 메커니즘
 
 #PostgreSQL의 대표적인 특징
  '신뢰도'는 제품의 최우선 사항
  ACID 및 트랜잭션 지원
  다양한 인덱싱 기법 지원
  유연한 Full-text search 기능
  동시성 성능을 높여주는 MVCC 기능
  다양하고 유연한 복제 방식 지원
  다양한 프로시져(PL/pgSQL, Perl, Python, Ruby, TCL, 등)/인터페이스(JDBC, ODBC, C/C++, .Net, Perl, Python, 등) 언어
  질 좋은 커뮤니티 지원 및 상업적인 지원
  잘 만든 문서 및 충분한 매뉴얼 제공
  
 #PostgreSQL만의 차별화된 확장 기능
  GIS add-on 지원 (PostGIS)
  Key-Value 스토어 확장 기능 (HStore)
  DBLink 기능
  Crypto, UUID 등 다양한 함수, 타입 지원
  
  <출처:https://d2.naver.com/helloworld/227936>
