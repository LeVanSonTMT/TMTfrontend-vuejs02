<template>
  <div class="body">
    <h1>Register account</h1>
    <div class= "form-check-in">
      <form action="" method="" @submit.prevent="register()">
        <div class="form-group">
          <label for="username">User name:</label>
          <input v-model="users.username" id="username" class="form-control" type="text" name="username" readonly> 
        </div>
        <div class="form-group">
          <label for="name" >Email:</label>
          <input  v-model="users.email" id="email" class="form-control" type="email" name="email" required> 
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input v-model="users.password" id="password" class="form-control" type="password" name="password" required> 
        </div>  
        <div class="form-group">
          <label for="name" >Name:</label>
          <input  v-model="users.name" id="name" class="form-control" type="text" name="name" required> 
        </div>
        <div class="form-group">
            <label for="id_type">Type account:</label>
            <select class="form-control" v-model="type_acc.id_type">
                <option :value="data.id" v-for="(data, i) in dataType_acc" :key="i">{{data.type_name}}</option>
            </select>
        </div>
        <button type ="submit" class="btn">Add User</button>
      </form>
    </div>
  </div>
</template>
  
<script>

const axios = require('axios');

export default (  {
  name: "register_account",
  data(){
    return{
      dataType_acc:[],
      users:{
        username:'',
        password:'',
        name:'',
        id_type:'',
        type_name: '',
      },
      errors:{}
    }
  },
  
  mounted(){
    this.register();
    this.checktype();
  },

  methods: {

    register: function(){        
      axios.post('http://127.0.0.1:8000/api/register', this.users)  
      .then( () => {
        alert("Đăng tí tài khoản thành công");
        window.location.reload();
      })
      .catch( () => {
        console.log("lỗi rồi!");
      });
    },
    checktype: function(){
      axios.get('http://127.0.0.1:8000/api/getType',{
      })
      .then(response => {
        this.dataType_acc = response.data;
        this.type_acc.id_type = response.data.id_type;
        console.log(this.dataType_acc);
      })
      .catch(() => {
        console.log('loi roi');
      })
    }
  } 
})
</script>

<style scoped>
  .body{
    padding: 10px;
    float: left;
    width: 100%;
  }

  h1 {
    background-clip: border-box;
    background:  #4CAF50;
    border-radius: 8px 8px 0px 0px;
    color: white;
    text-align: center;
    font-family: Tahoma, Verdana, sans-serif;
    font-size: 30px;
    padding: 5px;
    width: 50%;
    float: left ;
    overflow: auto;
  }
  
  .picker  {
    width: 100%;
    padding: 12px 20px;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

  .form-check-in {
    width: 50%;
    border-radius: 0px 0px 8px 8px;
    background-color: #f2f2f2;
    padding :20px;
    float: left ;
    overflow: auto;
    margin-right:20px ;
  }
  .card {
    position: relative;
    display: flex;
    flex-direction: column;
    min-width: 0;
    word-wrap: break-word;
    background-color: #fff;
    background-clip: border-box;
    border: 1px solid rgba(0, 0, 0, 0.125);
    border-radius: 0.25rem;
    Width: 40%;
  }

  .btn {
    width: 100%;
    background-color: #4CAF50;
    color: white;
    margin-bottom: 5px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  .btn:hover {
    background-color: #3e8e41;
  }

</style>
