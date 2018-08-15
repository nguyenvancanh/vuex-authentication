# Vuex Authentication

Vuex là gì? Bạn có thể hiểu một cách nôm na là Vuex được xây dựng dựa trên ý tưởng của Flux, Redux và kiến trúc Elm, tuy nhiên nó không được tích hợp vào trong core của vuejs mà nó được phát triển thành một package riêng. Vuex sinh ra giúp chúng ta quản lý các components trong project một cách đơn giản và hiệu quả. Nếu bạn không xây dựng một ứng dụng đơn trang và có lượng dữ liệu lớn thì không cần thiết sử dụng đến nó. Nhưng khi bạn làm việc với dữ liệu lớn thì Vuex sẽ là một giải pháp hữu ích cho bạn. Một bài viết về Vuex tương đối cụ thể và dễ  hiểu. Bạn có thể tham khảo [tại đây](https://techblog.vn/tai-sao-dung-vuex). 

Trong bài này, tôi không tập trung vào giải thích các khái niệm cũng như cách sử dụng của **Vuex**. Vì vậy, trước khi đọc bài này, các bạn cũng cần nắm qua một chút kiến thức về Vuex nhé.

Trong bài này, chúng ta sẽ tập trung vào việc sử dụng Vuex để xây dựng một ứng dụng Authentication. Trước tiên, cần chuẩn bị môi trường để code đã. Chúng ta sẽ sử dụng **vue-cli** để tạo mới projects. Để cài được **vue-cli** tham khảo tại link [Vue-cli](https://cli.vuejs.org/guide/). Sau khi đã cài đặt thành công **vue-cli** chạy command sau để  tạo mới project. 

```
vue create vue-auth
```
Tiếp theo, cài thêm package **Axios**

```
npm install axios --save
```
# Setup Axios

Chúng ta sẽ sử dụng axios trên nhiều components trong projects. Vì vậy chúng ta nên cài đặt nó ngay từ đầu để khi cần sử dụng tới chúng ta không phải code lại đoạn code đó nhiêu lần nữa. Thực hiện như sau: mờ file **./src/main.js** và thêm dòng code sau

```bash 
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import Axios from 'axios'

Vue.prototype.$http = Axios;

const token = localStorage.getItem('user-token')
if (token) {
  Vue.prototype.$http.defaults.headers.common['Authorization'] = token
}

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```
Từ giờ, khi bạn cần sử dụng axios trong components bất kỳ nào chỉ cần gọi **this.$http**

# Tạo Components

**Login Component** 
Trong folder _./src/components_ tạo file **Login.vue** với nội dung sau: 

```
<template>
 <div>
   <form class="login" @submit.prevent="login">
     <h1>Sign in</h1>
     <label>Email</label>
     <input required v-model="email" type="email" placeholder="Name"/>
     <label>Password</label>
     <input required v-model="password" type="password" placeholder="Password"/>
     <hr/>
     <button type="submit">Login</button>
   </form>
 </div>
</template>
```
Đây là template cho form login của bạn. Bạn cũng có thể tùy chỉnh form này theo ý thích. sau khi hoàn thành, hãy thêm tiếp thẻ script sau vào dưới thẻ template.

```
<script>
	export default {
		data(){
			return {
				email : "",
            	password : ""
            }
		},
		methods: {
		 	login: function () {
		   		let email = this.email 
		   		let password = this.password
		   		this.$store.dispatch('login', { email, password })
		   		.then(() => this.$router.push('/'))
		   		.catch(err => console.log(err))
		   	}
		}
	}
</script>
```

Ở đây, chúng ta đã sử dụng vuex action _ login để handle chức năng login.

**Register Component** 
Tương tự như login component, hãy tạo file **Register.vue** và thêm đoạn code sau:

```
<template>
  <div>
    <h4>Register</h4>
    <form @submit.prevent="register">
      <label for="name">Name</label>
      <div>
          <input id="name" type="text" v-model="name" required autofocus>
      </div>

      <label for="email" >E-Mail Address</label>
      <div>
          <input id="email" type="email" v-model="email" required>
      </div>

      <label for="password">Password</label>
      <div>
          <input id="password" type="password" v-model="password" required>
      </div>

      <label for="password-confirm">Confirm Password</label>
      <div>
          <input id="password-confirm" type="password" v-model="password_confirmation" required>
      </div>

      <div>
          <button type="submit">Register</button>
      </div>
    </form>
  </div>
</template>
```

Sau đó, định nghĩa data attribute, và thêm function register như sau:

```
<script>
    export default {
        data(){
            return {
                name : "",
                email : "",
                password : "",
                password_confirmation : "",
                is_admin : null
            }
        },
        methods: {
            register: function () {
                let data = {
                    name: this.name,
                    email: this.email,
                    password: this.password,
                    is_admin: this.is_admin
                }
                this.$store.dispatch('register', data)
               .then(() => this.$router.push('/'))
               .catch(err => console.log(err))
            }
        }
    }
</script>
```

**Secure Component**

Tương tự như 2 component ở trên, tạo component **Secure.vue** với nội dung

```
<template>
  <div>
    <h1>This page is protected by auth</h1>
  </div>
</template>
```

**Update The App Component**
