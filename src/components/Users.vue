<template>
  <div class="users right-side">
    <section class="content-header">
      <h1>
        用户列表
        <small>用户</small>
      </h1>
      <ol class="breadcrumb">
        <li><a href="/admin/index"><i class="fa fa-dashboard"></i> 管理中心</a></li>
        <li><a href="/admin/article">用户</a></li>
        <li class="active">用户列表</li>
      </ol>
    </section>

    <!-- Main content -->
    <section class="content">

      <div class="row">
        <div class="col-md-12">
          <div class="box">
            <div class="box-header">
              <h3 class="box-title"></h3>
              <router-link to="/admin/addUser" class="btn btn-default pull-right">添加用户</router-link>
            </div><!-- /.box-header -->
            <div class="box-body">
              <table class="table table-bordered  table-hover">
                <thead>
                <tr>
                  <th style="width: 10px">#</th>
                  <th>用户名</th>
                  <th>用户状态</th>
                  <th>用户组</th>
                  <th>工作量</th>
                  <th style="width: 20%">操作</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(item ,index) in users">
                  <td>{{ index+1 }}</td>
                  <td>{{ item.name }}</td>
                  <td>{{ item.status == 'inuse' ? '已启用' :'已禁用' }}</td>
                  <td>{{ item.roletype  }}</td>
                  <td>{{ item.taskNum != -1 ? item.taskNum :'查询错误'  }}</td>
                  <td>
                    <button class="btn" :class="item.status == 'inuse' ? 'btn-danger' :'btn-primary'" @click="editUser(item)">{{ item.status == 'inuse' ? '禁用' :'启用' }}</button>
                    <button class="btn btn-default" :disabled="item.status == 'inuse' ? false :true" @click="removeTask(item)" > 清除任务</button>
                  </td>
                </tr>
                </tbody>
              </table>
            </div><!-- /.box-body -->
            <div class="box-footer clearfix">
            </div>
          </div>
        </div>
      </div>
    </section><!-- /.content -->
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'Users',
    data () {
      return {
        msg: 'Welcome to Users',
        users: [],
        token:''
      }
    },
    methods: {
      editUser: function(item){
        var that = this
        var newStatus = item.status == 'inuse' ? 'notuse' : 'inuse'
        axios.post('/api/editUser' ,JSON.stringify({
          token:that.token,
          name:item.name,
          status: newStatus
        })).then(function(d){
          console.log(d)
          if(d.data.code == 1){
//            item = d.data.data
            item.status = newStatus
//            console.log('editUser',item)
          }
        })
      },
      removeTask: function(user){
        var that = this
        axios.post('/api/clearUserOwn' ,JSON.stringify({
          token:that.token,
          name:user.name
        })).then(function(d){
          if(d.data.code ==1){
            window.alert('清除任务成功')
          }
        })
      }
    },
    beforeMount: function(){
      var that = this
      var user = JSON.parse(this.$cookie.get('user'))
//      console.log('beforeMount:', axios)
      this.token = user.token
      axios.post('/api/userList' ,JSON.stringify({
        token:user.token
      })).then(function(d){
        console.log(d)
        if(d.data.code == 1){
          that.users = d.data.data.users
        }
      })

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
