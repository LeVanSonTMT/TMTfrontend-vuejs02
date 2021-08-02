<template>
 <div class="hold-transition login-page">
  <div class="Login">
    <h3>{{ msg }}</h3>
    
    <div class="login-box">
      <!-- /.login-logo -->
      <div class="card card-outline card-primary">
        <div class="card-header text-center">
          <a href="" class="h1"><b>Login</b></a>
        </div>
        <div class="card-body">
          <p class="login-box-msg">Sign in to start your session</p>

          <form @submit.prevent="login">
            <div class="input-group mb-3">
              <input type="email" class="form-control" placeholder="Email" v-model="email">
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-envelope"></span>
                </div>
              </div>
            </div>
            <div class="input-group mb-3">
              <input type="password" class="form-control" placeholder="Password" v-model="password">
              <div class="input-group-append">
                <div class="input-group-text">
                  <span class="fas fa-lock"></span>
                </div>
              </div>
            </div>
            <div class="row">
              <div class="col-8">
                <div class="icheck-primary">
                  <p class="mb-1" style="font-size:15px;">
                      <a href="https://frontendvuejs-v01.herokuapp.com/Forgot_Password">I forgot my password</a>
                  </p>
                </div>
              </div>
              
              <!-- /.col -->
              <div class="col-4">
                <button type="submit" @click="login()" class="btn btn-primary btn-block">Log In</button>
              </div>
              <!-- /.col -->
            </div>
          </form>

           <div class="social-auth-links text-center mt-2 mb-3">
            <button type="submit" @click="wgitlab()" class="btn btn-block btn-danger">
              <i class="fab fa-gitlab mr-2"></i> Sign in using Gitlab
            </button>
          </div>
          <!--  <a href="#" class="btn btn-block btn-danger">
              <i class="fab fa-google-plus mr-2"></i> Sign in using Google+
            </a>
          </div> -->
          <!-- /.social-auth-links -->
        </div>
        <!-- /.card-body -->
      </div>
      <!-- /.card -->
    </div>
    <!-- /.login-box -->
  </div>
  </div>
</template>

<script>
  const axios = require('axios');
  export default {
    name: 'Login',
    props: {
      msg: String
  },
  data () {
    return {
      email: '',
      password: ''
    }
  },

  methods: {
    login () {
      this.$store
        .dispatch('login', {
          email: this.email,
          password: this.password
        })
        .then(() => {
          console.log('is running...')
          this.$router.push({ name: 'admin' }) 
        })
        .catch(err => {
          console.log(err)
        })
    },
    created () {
      const userInfo = localStorage.getItem('user')
      if (userInfo) {
        const userData = JSON.parse(userInfo)
        this.$store.commit('setUserData', userData)
      }
    },
    // { 
    //           headers: {
    //       Authorization: 'Bearer ' + token //the token is a variable which holds the token
    //     }}
    wgitlab(){
      axios.get('https://backend-v01.herokuapp.com/api/login-gitlab',{headers: {"Access-Control-Allow-Origin": "*"}})
        .then( (res) => {
          console.log(res);          
          if(res.status == 201){
            //this.$router.push({ name: 'admin' }) 
          }  
        }).catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">


</style> 