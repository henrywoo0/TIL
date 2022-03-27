# Node.js로 웹서버 짜보기

## 기본 웹서버
```javascript
const http = require('http');
const server = http.createServer((request, response) => {
    response.writeHead(200, {'Content-Type': 'text/html'});
    response.end('Hello');
});
server.listen(3000);
```

## npm init
* 새 프로젝트를 만들어주는 가장 기본적인 명령어
* 기존의 low 레벨의 node.js 웹서버 개발 문제들을 해결할 수 있음

#### 관련 설정
* package name (디폴트는 파일 이름)
* version (디폴트 1.0.0)
* description
* entry point (시작점) `server.js`, `app.js`, `index.js` 등
* test command
* git repository
* keywords (이 프로젝트를 검색할 키워드)
* author (내 닉네임과 이메일 주소)
* license (저작권 관련, 디폴트 ISC)

#### Node.js로 해야 할 일은 너무 많다
* 라우팅
* Static resource 관리
* View rendering

## Express
Node.js를 이용해 웹 애플리케이션 서버를 구현하려고 할 때 필수 라이브러리

아래와 같은 편리한 기능 제공
* 라우팅
* Middleware
* Static resources
* View Template Engine & Folder
* …

위 세팅 설정 후 `express()`로 생성된 객체를 `http.createServer()`로 전달하면 웹서버 가동됨

## Project Scaffolding
* Node.js는 틀이 없어서 자유도가 높으나, 초보자에겐 더 어려움
* 기본적인 MVC *프로젝트의 뼈대*를 잡아주는 라이브러리
* Express generator -> `npm`, `npx`  두 가지가 있음

#### `npm` vs `npx`
* `npm` : 디스크에 전역으로 다운로드
* `npx` : 일회성 다운로드

`npx` 명령어 : `npx express-generator --view=pug myserver`
Express-generator를 사용하면 라이브러리 버전이 낮아 `package.json` 변경 필요

```json
{
  "name": "myserver",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "cookie-parser": "~1.4.6",
    "debug": "~4.3.3",
    "express": "~4.17.2",
    "http-errors": "~2.0.0",
    "morgan": "~1.10.0",
    "pug": "3.0.2"
  }
}
```

## Pug와 express로 라우터 만들기
1. Views 폴더에 pug 파일 추가
2. Routes 폴더에 해당 라우터 추가
3. App.js에서 주소와 라우터 연결


