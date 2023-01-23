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

### 개발용 라이브러리 와 배포용 라이브러리
* npm i ~~~  or npm install ~~~ --save-prod
  * 이렇게 설치된 배포용 라이브러리는 npm run build로 빌드를 하면 최종 애플리케이션 코드 안에 포함됩니다.
* npm i ~~~ -D or npm install ~~~ --save-dev
  * 설치 옵션에 -D를 주었다면 해당 라이브러리는 빌드하고 배포할 때 애플리케이션 코드에서 빠지게 됩니다. 
  * 따라서, 최종 애플리케이션에 포함되어야 하는 라이브러리는 -D로 설치하면 안 됩니다.

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

### computed
* Vue data 변화시 발생하는 함수를 정의 하는곳
  ~~~
  // vue 인스턴스 내부에 username이 변경될때마다 isUsernameValid 함수 실행됨
  computed: {
    isUsernameValid() {
      return validateEmail(this.username);
    },
  },
  ~~~
### this.$router.push('/main');
* javascript 태그 안에서 url 및 페이지 변경 object 및 파라미터를 넘길 수 있습니다.
* https://router.vuejs.org/guide/essentials/navigation.html
   ~~~
   this.$router.push('/main');
   ~~~
  
### 컴포넌트간 데이터 전달 방법 3가지
1. component 통신 방식 props 와 event를 이용
2. event bus를 이용하여 데이터를 전달
3. vuex 이용하여 store object를 이용
   1. vuex 라이브러리를 다운받아 vue프로젝트 내에 데이터 변경을 한곳에서 관리를 할 수 있다.
   2. mutations라는 메소드를 이용해 데이터를 사용한다.
   3. this.$store.commit(메소드명 , 전달 값)을 이용해 store내부에 있는 state 안에 값이 들어온다.
   4. {{ $store.state.username }} 같이 사용하여 값을 html내부에 표기 할 수 있다.
   ~~~
   export default new Vuex.Store({
    state: {
    username: '',
    },
    getters: {
    isLogin(state) {
    return state.username !== '';
    },
    },
    mutations: {
    setUsername(state, username) {
    state.username = username;
    },
    clearUsername(state) {
    state.username = '';
    },
    },
    });
   ~~~
    

### vue 메서드
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
3. v-bind:속성
   * v-bind를 이용해 html속성애 따라 활성화 시킬 수 있다.
   ~~~
   : <- v-bind 축약어 FALSE일때 disabled됨
   :disabled="!isUsernameValid || !password"
   ~~~
   
