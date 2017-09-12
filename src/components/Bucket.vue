<template>
  <div class="bucket right-side">
    <section class="content-header">
      <h1>
        Buckets列表
        <small>Buckets</small>
      </h1>
      <ol class="breadcrumb">
        <li><a href="/admin/index"><i class="fa fa-dashboard"></i> 管理中心</a></li>
        <li><a href="/admin/article">Buckets</a></li>
        <li class="active">Buckets列表</li>
      </ol>
    </section>
    <!-- Main content -->
    <section class="content">
      <div class="row">
        <div class="col-md-12">
          <div class="box">
            <div class="box-header">
              <h3 class="box-title"></h3>
              <a href="javascript:void(0)" class="btn btn-default pull-right " @click="downloadReport">导出标注进度报告</a>
              <!--<a href="javascript:void(0)" class="btn btn-default pull-right">添加Buckets</a>-->
            </div><!-- /.box-header -->
            <div class="box-body">
              <table class="table table-bordered  table-hover">
                <thead>
                  <tr>
                    <th style="width: 10px">#</th>
                    <th>bucket</th>
                    <th>类型</th>
                    <th>标注进度</th>
                    <th>已标注</th>
                    <th>总量</th>
                    <th style="width: 20%">备注</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(item ,index) in buckets">
                    <td>{{ index+1 }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ JSON.stringify(item.buckettypes).replace(/\[/g,'').replace(/\]/g,'') }}</td>
                    <td>{{ (item.annotatedfilenum / item.totalfilenum) * 100 + "%" }}</td>
                    <td>{{ item.annotatedfilenum != -1 ? item.annotatedfilenum : '查询错误'}}</td>
                    <td>{{ item.totalfilenum != -1 ? item.totalfilenum : '查询错误'}}</td>
                    <td>
                      <!--<a class="btn btn-default" title="删除" onclick="return confirm('是否删除？');"><span class="fa fa-trash-o"></span> 删除</a>-->
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
    <iframe src="" frameborder="0" class="hide" id="downloadIframe"></iframe>
  </div>

</template>

<script>
  import axios from 'axios'
export default {
  name: 'Bucket',
  data () {
    return {
      msg: 'Welcome to Bucket',
      buckets: [],
      download: ''
    }
  },
  methods:{
    downloadReport:function(){
//      this.download = '/static/js.tar.gz'
      var user = JSON.parse(this.$cookie.get('user'))
      axios.post('/api/exportReport' ,JSON.stringify({
        token:user.token
      })).then(function(d){
        console.log(d)
        if(d.data.code == 1){
          document.getElementById('downloadIframe').src = d.data.data.url
        }
      })
//      document.getElementById('downloadIframe').src = '/static/js.tar.gz'
    }
  },
  beforeMount: function(){
    var that = this
    var user = JSON.parse(this.$cookie.get('user'))
    //      console.log('beforeMount:', axios)
    axios.post('/api/bucketReport' ,JSON.stringify({
      token:user.token
    })).then(function(d){
      console.log(d)
      if(d.data.code == 1){
        that.buckets = d.data.data.buckets
      }
    })

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
