### jsonconfig.json
* @ 절대경로 단축키 등록 빌드 등록 빌등 exlude 등록
### eslintrc.js
* prettier와 같이 있음 rules : []

### vue .env
1. .env  , .env.development , .env.production 3가지를 지원한다.
   1. localhost 빌드시 .dev elopment 사용 npm run build 후 사용시 production사용 두 env파일내에 값이 없을때 .env파일을 사용하게 된다.
2. VUE_APP_API_URL = http://localhost:3000/ VUE_APP 접미사를 붙이면 vue 프로젝트 내에서 자동으로 .env파일을 로드해준다.
   ~~~
   const instance = axios.create({
   baseURL: process.env.API_URL, // .env파일 내에 VUE_APP이라 작성한다면 자동으로 env 파일 내에서로드됨
   });
   ~~~
### 코드 스플리팅
* url에 맞춰 해당 컴포넌트를 들고 동적으로 들고 오는 방법
  ~~~
  routes: [
    { path: '/login', component: () => import('@/views/LoginPage') },
    { path: '/signup', component: () => import('@/views/SignupPage') },
  ],
  ~~~
  
### 없는 페이지 요청 접근
* router index 안 path:'*' <- 이외 모든 접근에 대하여 반응합니다.

### axios 구조화
* src/api 안에 axios 관련 데이터를 구조화하여 사용합니다.

### vue
1. router-link
   ~~~
    <router-link to="/signup">회원가입</router-link> // to에 있는 url이 매핑이 되면 routerView라는 위치에 html을 위치 시켜준다
    <router-view></router-view>
   ~~~
2. v-model
   * v-model이라는 속성을 사용하면 입력 값이 자동으로 뷰 데이터 속성에 연결됩니다.
   * v-bind , v-on이라는 속성과 같이 이용이 됩니다.
   ~~~~
   data() {
    return {
      username: '',
      password: '',
      nickname: '',
    };
    },
   ~~~~
   * @submit.prevent :submit 버튼에 대한 이벤트 x prevent @ v-??
