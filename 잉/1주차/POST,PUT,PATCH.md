## Warm-up
###문제1. 
GET 메서드와 POST 메서드의 차이점은?

###문제2.
POST 메서드, PUT 메서드, PATCH 메서드의 차이점은? 


###답1.
GET: 서버의 리소스에서 데이터를 요청할 때 사용    
- 리소스를 조회한다는 점에서 여러 번 요청하더라도 응답이 똑같기 때문에 멱등하다. 

POST: 서버의 리소스를 새로 생성/업데이트 시 사용  
- 리소스 생성/업데이트 용도이기 때문에 멱등이 아니다. 

Indempotent(멱등)
: 몇 번을 실행하더라도 같은 값이 나온다. 라는 의미 

###답2.  
POST와 PATCH는 Idempotent하지 않고, PUT은 Indempotent한 메서드이다.  
POST나 PUT은 일부를 수정할 수 있는 만큼 값이 변할 가능성이 있지만,  
PUT은 몇 번을 실행하더라도 아예 데이터를 대체해버리기 때문에 멱등한 것이다.  

####정리
POST -> CREATE  
PUT -> REPLACE  
PATCH -> UPDATE   

##START

### POST
- 식별자(Identifier) 없이 Data가 들어오면 새 식별자를 생성하고 Data를 등록 
- 식별자 없는 Data가 또 들어오면 새 식별자를 또 생성하고 Data를 등록

example)  
**Request.**
```
POST /crew
{
    "name": "까라",
    "speciality": "가스라이팅"
}

```
**Response.**
```
HTTP/1.1 200 OK
{
    "id": "1",
    "name": "까라",
    "speciality": "가스라이팅"
}
```

 ```
 HTTP/1.1 200 OK

{
    "id": "2",
    "name": "까라",
    "speciality": "가스라이팅"
}
```



### PUT
- Data가 들어왔을 때 식별자가 존재하면 해당 리소스를 업데이트(Replace).
- Data가 들어왔을 때 식별자가 존재하지 않으면 새 식별자를 생성하고 Data를 등록.

example)   
**Request.**
```
PUT /crew
{
    "id":1,
    "name": "까라",
    "speciality": "가스라이팅"
}

```
**Response.**
```
HTTP/1.1 200 OK
{
    "id": "1",
    "name": "까라",
    "speciality": "가스라이팅"
}
```
기존 데이터가 없으면 새로 생성하고, 있으면 대체해준다.   
항상 같은 값이 나올 것이다. 

### PATCH 
- POST와 PUT을 섞은 느낌 
- Data가 들어왔을 때 식별자가 존재하면 해당 리소스를 업데이트한다. 
- Data가 들어왔을 때 식별지가 존재하지 않으면 Exception이 터진다.

example)  
**Request.**
```
PATCH /crew
{
    "id":1,
    "name": "썬",
}

```
**Response.**
```
HTTP/1.1 200 OK
{
    "id": "1",
    "name": "썬",
    "speciality": "가스라이팅"
}
``` 