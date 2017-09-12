<template>
  <div>
    <header class="header">
      <nav class="navbar navbar-static-top" role="navigation">
        <a href="#" class="navbar-btn sidebar-toggle" data-toggle="offcanvas" role="button">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </a>
        <div class="navbar-right">
          <ul class="nav navbar-nav">

            <!-- User Account: style can be found in dropdown.less -->
            <li class="dropdown user user-menu">
              <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                <i class="glyphicon glyphicon-user"></i>
                <span>{{user.name}} <i class="caret"></i></span>
              </a>
              <ul class="dropdown-menu">
                <li class="user-header bg-light-blue">
                  <img src="/static/img/avatar04.png" class="img-circle" alt="User Image" />
                  <p>
                    Beyondsoft - {{user.name}}
                    <small>登陆于2016年01月01日</small>
                  </p>
                </li>
                <li class="user-footer">
                  <div class="pull-left">
                    <a href="#" class="btn btn-default btn-flat">用户信息</a>
                  </div>
                  <div class="pull-right">
                    <a href="#" class="btn btn-default btn-flat" @click="logout()">注销登陆</a>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </nav>
    </header>
    <div class="wrapper row-offcanvas row-offcanvas-left">
      <aside class="left-side sidebar-offcanvas">
        <section class="sidebar">
          <div class="user-panel">
            <div class="pull-left image">
              <img src="/static/img/avatar04.png" class="img-circle" alt="User Image" />
            </div>
            <div class="pull-left info">
              <p>Hello, {{user.name}}</p>
              <a href="#"><i class="fa fa-circle text-success"></i> 在线</a>
            </div>
          </div>
          <form action="#" method="get" class="sidebar-form">
            <div class="input-group">
              <input type="text" name="q" class="form-control" placeholder="操作"/>
              <span class="input-group-btn">
                  <button type='submit' name='search' id='search-btn' class="btn btn-flat"><i class="fa fa-search"></i></button>
              </span>
            </div>
          </form>
          <ul class="sidebar-menu">
            <li class="active">
              <router-link to="/admin">
                <i class="fa fa-dashboard"></i> <span>控制台</span>
              </router-link>
            </li>
            <li class="treeview">
              <a href="#">
                <i class="fa fa-th-large"></i> <span>用户管理</span>
                <i class="fa fa-angle-left pull-right"></i>
              </a>
              <ul class="treeview-menu">
                <li><router-link to="/admin/users"><i class="fa fa-list"></i>用户列表</router-link></li>
                <li><router-link to="/admin/addUser"><i class="fa fa-edit"></i>用户添加</router-link></li>
              </ul>
            </li>
            <li class="treeview">
              <a href="#">
                <i class="fa fa-file"></i> <span>Bucket管理</span>
                <i class="fa fa-angle-left pull-right"></i>
              </a>
              <ul class="treeview-menu">
                <li><router-link to="/admin/bucket"><i class="fa fa-list"></i>Bucket列表</router-link></li>
                <!--<li><router-link to="/admin/addBucket"><i class="fa fa-edit"></i>Bucket添加</router-link></li>-->
              </ul>
            </li>
          </ul>
        </section>
        <!-- /.sidebar -->
      </aside>
      <router-view></router-view>
      <section class="content-footer">
        <div class="text-center">
          © 2016 All Rights Reserved. Beyondsoft
        </div>
      </section><!-- /.content-footer -->
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'Admin',
  data () {
    return {
      user: {
        name: '',
        loginTime: null
      },
      token: ''
    }
  },
  methods: {
    logout: function () {
      debugger
      var that = this
      that.$cookie.delete('user')
      window.location.href = '#/login'
//      axios.post('/api/logout', JSON.stringify({token: that.token}))
//        .then(function (msg) {
//          that.$cookie.delete('user')
//        })
//        .catch(function (err) {
//          console.log('logout', err)
//        })
    }
  },
  beforeCreate: function () {
    var that = this
    var user = JSON.parse(that.$cookie.get('user'))
//    console.log('admin beforeCreate',user)

  },
  beforeMount: function () {
    var that = this
    var user = JSON.parse(that.$cookie.get('user'))
    console.log('admin beforeMount', user)

//    console.log(user.token)
//    debugger
    if (user && user.token ) {
      that.token = user.token
      that.user.name = user.name
      that.user.loginTime = new Date(user.name)
    } else {
      window.location.href = '#/login'
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
