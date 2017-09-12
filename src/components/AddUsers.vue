<template>
  <div class="addUsers right-side">
    <section class="content-header">
      <h1>
        用户添加
        <!--<small>用户</small>-->
      </h1>
      <ol class="breadcrumb">
        <li><router-link to="/admin"><i class="fa fa-dashboard"></i> 管理中心</router-link></li>
        <li><router-link to="/admin/users">用户</router-link></li>
        <li class="active">用户添加</li>
      </ol>
    </section>

    <!-- Main content -->
    <section class="content">
      <div class="row">
        <div class="col-md-12">
          <div class="box">
            <div>
              <div class="box-header">
                <h3 class="box-title"></h3>
                <router-link to="/admin/addUser">用户添加</router-link>
              </div>
              <!-- /.box-header -->
              <div class="box-body">
                <div class="form-horizontal">
                  <div class="form-group">
                    <label for="inputSubject" class="col-sm-2 control-label">用户名称</label>
                    <div class="col-sm-10">
                      <input type="text" name="title" placeholder="用户名称" id="inputSubject" class="form-control " v-model="user.name">
                    </div>
                  </div>
                  <div class="form-group">
                    <label for="userpwd" class="col-sm-2 control-label">用户密码</label>
                    <div class="col-sm-10">
                      <input type="text" name="title" placeholder="用户密码" id="userpwd" class="form-control" v-model="user.passwd">
                    </div>
                  </div>
                  <div class="form-group">
                    <label for="usetypes" class="col-sm-2 control-label">用户类型</label>
                    <div class="col-sm-10">
                      <select type="text" name="types" id="usetypes" class="form-control" v-model="user.roletype">
                        <option disabled value="">请选择</option>
                        <option v-for="rol in role" :value="rol.type">{{rol.type}}</option>
                      </select>
                    </div>
                  </div>
                  <div class="form-group">
                    <div class="col-sm-offset-2 col-sm-10">
                      <div class="checkbox">
                        <label for="userKey">
                          <input type="checkbox" name="userKey" id="userKey" v-model="user.preStatus" >状态
                        </label>
                      </div>
                    </div>
                  </div>
                  <div class="box-footer clearfix">
                    <div class="col-sm-offset-2 col-sm-10">
                      <button class="btn btn-primary" @click="submit">提交</button>
                    </div>
                  </div>
                  <!--<button class="btn btn-info" type="submit" name="submit" value="save">仅保存</button>-->
                </div>
              </div>

            </div>

          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'AddUser',
    data () {
      return {
        msg: 'Welcome to Add Users',
        user:{
          name: '',
          passwd: '',
          preStatus: true,
//          status: 'inuse',
          roletype: 'annotater'
        },
        role:[
          { code:1,type:'annotater'},
          { code:2,type:'expert'},
          { code:3,type:'webadmin'}
        ]
      }
    },
    methods:{
      submit:function(){
        var that = this
        that.user.status = that.user.preStatus ? 'inuse' : 'notuse'
        that.user.token = JSON.parse(that.$cookie.get('user')).token
        axios.post('/api/createUser',JSON.stringify(that.user))
          .then(function(msg){
            if(msg.data.code == 1 ){
              window.alert('添加成功')
              setTimeout(function(){
                window.location.href = '#/admin/users'
              },2000)

            }
          })
      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
