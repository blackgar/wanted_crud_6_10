# 원티드 프리온보딩 프론트엔드 6차 10팀 week1-1 과제

## 프로젝트 설명
### 프로젝트 개요
- 프리온보딩 사전 과제를 새롭게 처음부터 구현해보면서 사전 과제를 진행할 때 부족했던 부분을 보완하고 모듈화와 최적화를 진행한 프로젝트입니다. 또한, 로그인과 회원가입 기능을 하나로 통합하여 훨씬 높은 UX를 제공할 수 있게 기능 구현을 하였습니다.(Wanted 로그인 시스템 참고)
### 컴포넌트 설계
src
├─api  // api요청 관련 모든 함수 정리
│  └─axios.jsx // 규모가 작은 프로젝트라 하나의 파일로 정리. 규모가 커질 경우 기능별 파일로 분할 진행
├─components // 공통으로 사용되는 component. 작은 규모의 프로젝트라 Pages에 들어가는 Component들을 세분화 진행하지 않음
│  ├─Button.jsx
│  └─Input.jsx
├─pages // 기능별 페이지
│  ├─Auth 
│  │  └─Auth.jsx // 로그인과 회원가입 코드
│  └─Todo 
│     ├─CreateTodo.jsx // Todolist 생성 코드
│     ├─Todo.jsx // Todolist 관련 api 요청 및 state 관리 코드
│     ├─TodoList.jsx // Todolist 코드
│     └─TodoListItem.jsx // Todolist 수정/삭제/완료 코드
├─styles
│  ├─GlobalStyle.jsx // 전체 프로젝트 스타일 적용 코드
│  └─authstyle.js // 파일별로 사용하는 스타일 코드 모음
├─App.jsx
├─index.jsx
└─Routes.jsx // Routing을 위한 코드

## Skill
- React
- Styled-components
- react-router-dom
- mui/material
- sweetalert2

## 기능

### 1. 로그인/회원가입

- 전체적으로 푸른색과 하얀색으로 깔끔하고 편안한 느낌을 주는 UI로 구성
- 높은 UX를 제공하기 위해 이메일 입력시 가입한 이메일이면 비밀번호 입력창으로 이동하고 가입되어 있지 않은 이메일이면 회원가입창으로 이동할 수 있게 구현
- 따로 이메일만 확인할 수 있는 API가 없어 이메일과 임의 비밀번호 값(8자리 미만 비밀번호)을 axios 요청해 statusCode 401을 반환받게 되면 가입되어 있는 이메일이라는 response라는 것을 활용해 401을 반환받았을 때는 비밀번호를 입력하는 창으로 이동시키고 statusCode 404를 받아 가입되어 있지 않은 이메일인 경우 회원가입을 하도록 구현
- 최초 이메일 입력시 정규식을 통한 이메일 유효성 확인 => 유효성이 확인될 경우 Email로 계속하기 버튼 활성화 구현
- 이메일 입력 후 나오는 비밀번호 입력창에서 비밀번호를 틀려 401을 반환받게 되면 비밀번호 오류 알림 구현
- 회원가입 페이지에서 비밀번호 유효성 검사
- 회원가입 페이지에서 기존에 입력했던 이메일을 가입된 이메일로 변경할 경우 동일한 유저가 존재한다는 알림 구현
#### 로그인 성공
![로그인성공](https://user-images.githubusercontent.com/79856086/187743903-e6ecd88e-0a5d-428d-9b4f-c6fd618df41f.gif)
#### 로그인 비밀번호 체크
![로그인 비밀번호 체크](https://user-images.githubusercontent.com/79856086/187743940-04f605cd-2ae3-4e70-899b-aea0e7dd0157.gif)
#### 회원가입
![회원가입](https://user-images.githubusercontent.com/79856086/187744014-05965a40-8ce0-41bd-a834-efee46218915.gif)
#### 회원가입창 내 정보 변경시 가입 실패 안내
![회원가입창에서 정보 변경시 가입실패안내(동일한 이메일)](https://user-images.githubusercontent.com/79856086/187744083-e528aa3f-6e52-4176-ad5b-dd26762fc5fe.gif)

### 2. TodoList

#### 1)Todo 등록

- Todolist의 경우 상단 박스에 할 일을 입력하고 + 버튼을 누르거나 enter을 누를 경우 Todo가 등록되게 구현
- 빈값 입력시 Todo 추가되지 않게 구현
![createTodo](https://user-images.githubusercontent.com/79856086/187746509-5b54855c-6939-4b29-9527-b88fd93a0c46.gif)

#### 2)Todo 수정

- Todolist의 우측 수정 버튼을 통해 생기는 박스에서 바로바로 변경되는 값을 확인하면서 수정할 수 있도록 구현
- 수정완료 시 진짜 수정할 것인지에 대한 알림을 통해 확인기능 구현
- 수정을 하지 않을 때는 취소할 수 있는 취소 버튼 구현

#### 3)Todo 삭제

- Todolist 우측 삭제 버튼을 통해 Todo 삭제 기능 구현
- 삭제 시 진짜 삭제할 것인지에 대한 알림을 통한 확인기능 구현
- 삭제 하지 않을 때는 취소버튼을 통해 삭제하지 않을 수 있는 기능 구현

#### 4)Todo 완료

- Todolist 좌측 체크박스를 통해 Todo 완료 여부 표시 기능 구현
- 체크할 경우 완료된 상태로 변경되었다는 알림 표시 및 Todo 중간선 구현
#### Todo 수정/완료/삭제
![투두리스트](https://user-images.githubusercontent.com/79856086/187746491-017d48f1-3da6-4c61-bc57-d0cc54c09cda.gif)


## 실행 방법

```
npm i
npm start
```
