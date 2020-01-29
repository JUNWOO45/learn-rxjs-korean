# ajax

#### signature: `ajax(urlOrRequest: string | AjaxRequest)`

## URL, 헤더 등을 사용하여 요청 객체를 사용하거나 URL의 문자열을 사용하여 Ajax 요청에 대한 옵저버블을 생성합니다.

### 예시

**예시 1: 요청(request)으로부터 반환되는 응답(response) 객체를 내보내는 옵저버블.**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-raqi89) \)

```javascript
// RxJS v6+
import { ajax } from 'rxjs/ajax';

const githubUsers = `https://api.github.com/users?per_page=2`;

const users = ajax(githubUsers);

const subscribe = users.subscribe(
  res => console.log(res),
  err => console.error(err)
);

/* 결과
{  
  "originalEvent":{  
    "isTrusted":true
  },
  "xhr":{  

  },
  "request":{  
    "async":true,
    "crossDomain":true,
    "withCredentials":false,
    "headers":{  

    },
    "method":"GET",
    "responseType":"json",
    "timeout":0,
    "url":"https://api.github.com/users?per_page=2"
  },
  "status":200,
  "responseType":"json",
  "response":[  
    {  
      "login":"mojombo",
      "id":1,
      "node_id":"MDQ6VXNlcjE=",
      "avatar_url":"https://avatars0.githubusercontent.com/u/1?v=4",
      "gravatar_id":"",
      ...
    },
    {  
      "login":"defunkt",
      "id":2,
      "node_id":"MDQ6VXNlcjI=",
      "avatar_url":"https://avatars0.githubusercontent.com/u/2?v=4",
      "gravatar_id":"",
      "...
    }
  ]
}
*/
```

**예시 2: 요청으로부터 반환되는 응답 객체의 json 키 값만을 내보내는 옵저버블.**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-8jkrhl) \)

```javascript
// RxJS v6+
import { ajax } from 'rxjs/ajax';

const githubUsers = `https://api.github.com/users?per_page=2`;

const users = ajax.getJSON(githubUsers);

const subscribe = users.subscribe(
  res => console.log(res),
  err => console.error(err)
);

/* output
[  
  {  
    "login":"mojombo",
    "id":1,
    "node_id":"MDQ6VXNlcjE=",
    "avatar_url":"https://avatars0.githubusercontent.com/u/1?v=4",
    "gravatar_id":"",
    "...
  },
  {  
    "login":"defunkt",
    "id":2,
    "node_id":"MDQ6VXNlcjI=",
    "avatar_url":"https://avatars0.githubusercontent.com/u/2?v=4",
    "gravatar_id":"",
    ...
  }
]
*/
```

**예시 3: 요청으로부터 반환되는 에러 객체를 내보내는 옵저버블.**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-vnxkth) \)

```javascript
// RxJS v6+
import { ajax } from 'rxjs/ajax';

const githubUsers = `https://api.github.com/error`;

const users = ajax.getJSON(githubUsers);

const subscribe = users.subscribe(
  res => console.log(res),
  err => console.error(err)
);

/* 결과
Error: ajax error 404
*/
```

**예시 4: 객체를 포함한 Ajax 연산자.**

\( [StackBlitz](https://stackblitz.com/edit/rxjs-vqnnot) \)

```javascript
// RxJS v6+
import { ajax } from 'rxjs/ajax';

const githubUsers = `https://api.github.com/error`;

const users = ajax({
  url: githubUsers,
  method: 'GET',
  headers: {
    /*헤더 입력*/
  },
  body: {
    /*바디 입력*/
  }
});

const subscribe = users.subscribe(
  res => console.log(res),
  err => console.error(err)
);
```

### 추가 자료

* [ajax](https://rxjs.dev/api/ajax/ajax) :newspaper: - 공식 문서

> :file\_folder: Source Code: [https://github.com/ReactiveX/rxjs/blob/6.4.0/src/internal/observable/dom/ajax.ts\#L20-L19](https://github.com/ReactiveX/rxjs/blob/6.4.0/src/internal/observable/dom/ajax.ts#L20-L19)

