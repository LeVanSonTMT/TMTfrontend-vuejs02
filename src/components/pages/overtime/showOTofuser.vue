<template>
<!-- // Le_Van_Son -->
    <div class="container">
        <h1>Các đơn đã đăng ký</h1>
        <div class="table-responsive">
            <table class="table table-striped table-hover">
                <thead>
                    <tr>
                        <th>STT</th>                        
                        <th>Số giờ</th>
                        <th>Lý do làm thêm</th>
                        <th>Ngày Đăng Ký</th>
                        <th>Trạng thái</th>
                    </tr>
                </thead>
                <tbody>                    
                    <tr v-for="(data, i) in dataOvertime0" :key="i"> 
                        <td v-text="i+1">  </td>
                        <td>{{data.number}}</td>
                        <td>{{data.reason}}</td>
                        <td>{{data.ngayDK}}</td>
                        <td>
                          <a :href="'https://frontendvuejs-v01.herokuapp.com/EditOvertime/'+data.id"  class='btn btn-warning' ><i class="fas fa-pencil-alt"></i> Sửa </a>
                          <a href="" class='btn btn-danger' @click.prevent="click_detroy(data.id)" ><i class="fas fa-trash"></i> Xóa </a>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h1>Các đơn đã duyệt</h1>
        <div class="table-responsive">
            <table class="table table-striped table-hover">
                <thead>
                    <tr>
                        <th>STT</th>                        
                        <th>Số giờ</th>
                        <th>Lý do làm thêm</th>
                        <th>Ngày Đăng Ký</th>
                        <th>Ngày duyệt</th>
                        <th>Người duyệt</th>
                        <th>Trạng thái</th>
                    </tr>
                </thead>
                <tbody>                    
                    <tr v-for="(data, i) in dataOvertime1" :key="i"> 
                        <td v-text="i+1">  </td>
                        <td>{{data.number}}</td>
                        <td>{{data.reason}}</td>
                        <td>{{data.ngayDK}}</td>
                        <td>{{data.approved_time}}</td>
                        <td>{{ data.name_admin }}</td>
                        <td><span class="badge badge-success">Đã duyệt</span></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    
</template>

<script>

const axios = require('axios');

export default ({
   data() {
    return{
      dataOvertime0: [],
       dataOvertime1: [],
    }
    },

  mounted(){    
    this.checklogin();

  },

  methods:{
    checklogin: function(){
        var id_user =  JSON.parse(localStorage.getItem('user')).user.id; 
        // console.log('s : ', id_user);
        axios.get('https://backend-v01.herokuapp.com/api/showOT/'+id_user,{
        })
        .then( response => {
            this.dataOvertime0 = response.data[0];        
            this.dataOvertime1 = response.data[1];
            // console.log(this.dataOvertime);

        })
        .catch( () => {
            console.log('loi roi');
        })

    },

    click_detroy: function(id){
        axios.get('https://backend-v01.herokuapp.com/api/destroyOT/'+id,{
            
        })
        .then( res => {
          alert("Đã xóa thành công!");
          console.log(res.data);
          window.location.reload();
        })
        .catch( () => {
          console.log('loi roi');
        })
    },
   

  }

})
</script>
