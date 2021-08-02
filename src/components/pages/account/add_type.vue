<template>
  <div class="body">
    <h1>Add type account</h1>
    <div class= "form-check-in">
      <form action="" method="" @submit.prevent="add()">
        <div class="form-group">
          <label for="username">Type name:</label>
          <input v-model="type_acc.type_name" id="type_name" class="form-control" type="text" name="type_name" readonly> 
        </div>
        <button type ="submit" class="btn">Add Type</button>
      </form>
    </div>
  </div>
</template>
  
<script>

const axios = require('axios');

export default (  {
  name: "add_type",
  data(){
    return{
      dataType_acc:[],
      users:{
        type_name:'',
      },
      errors:{}
    }
  },
  
  mounted(){
    this.add_type();
  },

  methods: {
    add_type: function(){        
      axios.post('http://127.0.0.1:8000/api/storeType')  
      .then( () => {
        alert("Thêm loại tài khoản thành công");
        window.location.reload();
      })
      .catch( () => {
        console.log("lỗi rồi!");
      });
    },
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
