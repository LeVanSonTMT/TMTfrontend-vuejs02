<template>
    <div class="container">   
    <div class="card">
        <div class="card-header">
          <h3 class="card-title">Quản lý nghỉ phép</h3>

          <div class="card-tools">
            <button type="button" class="btn btn-tool" data-card-widget="collapse" title="Collapse">
              <i class="fas fa-minus"></i>
            </button>
            <button type="button" class="btn btn-tool" data-card-widget="remove" title="Remove">
              <i class="fas fa-times"></i>
            </button>
          </div>
        </div>
        <div class="card-body p-0 table-responsive">
          <table class="table table-striped table-hover projects">
              <thead>
                  <tr>
                      <th>
                          STT
                      </th>
                      <th>
                          Tên nhân viên
                      </th>
                      <th>
                          Ngày xin phép
                      </th>
                      <th>
                        Số ngày nghỉ
                      </th>
                      <th>
                          Lý do nghỉ
                      </th>
                      <th>
                          Thao tác
                      </th>
                  </tr>
              </thead>
              <tbody>
                  <tr v-for="(data, i) in dataDayOff" :key="i">
                      <td v-text="i+1">
                      </td>
                      <td>
                         {{data.name}}
                      </td>
                      <td>
                          {{data.start_off}}
                      </td>
                      <td>
                          {{data.num_off}}
                      </td>
                      <td >
                         {{data.off_reason}}
                      </td>
                      <td class="project-actions">
                          <a :href="'https://frontendvuejs-v01.herokuapp.com/Dayoff_edit/'+data.id" class="btn btn-warning btn-sm"><i class="fas fa-pencil-alt"></i> Sửa </a>
                          <a href="" class="btn btn-success btn-sm" @click.prevent="click_apply(data.id)" ><i class="fas fa-clipboard-check"></i> Duyệt </a>
                          <a href="" class="btn btn-danger btn-sm" @click.prevent="click_detroy(data.id)" ><i class="fas fa-trash"></i> Xóa </a>
                      </td>
                  </tr>
              </tbody>
          </table>
        </div>
        <!-- /.card-body -->
      </div>
      <!-- /.card -->
    </div>
</template>

<script>
    const axios = require('axios');

export default ({
   data() {
    return{
      dataDayOff: [],
      user_localstore:{
        admin_id:'',
        
      }
    }
    },

  mounted(){    
    this.checklogin();
  },

  methods:{
    checklogin: function(){
      axios.get('https://backend-v01.herokuapp.com/api/get-data/',{
      })
      .then( response => {
        this.dataDayOff = response.data;        
        this.user_localstore.admin_id =  JSON.parse(localStorage.getItem('user')).user.id; 
        
      })
      .catch( () => {
        console.log('Đã xảy ra lỗi');
      })
    },

    click_apply: function(id){
        axios.post('https://backend-v01.herokuapp.com/api/approved-dayoff/'+id,
            this.user_localstore
        )
        .then( res => {
          alert("Đã duyệt thành công!");
          console.log(res.data);
          window.location.reload();         

        })
        .catch( () => {
          console.log('Đã xảy ra lỗi');
        })
    },

    click_detroy: function(id){
        axios.get('https://backend-v01.herokuapp.com/api/cancel-dayoff/'+id,{
            
        })
        .then( res => {
          alert("Đã xóa thành công!");
          console.log(res.data);
          window.location.reload();
        })
        .catch( () => {
          console.log('Đã xảy ra lỗi');
        })
    },
  }
})
</script>
<style></style>