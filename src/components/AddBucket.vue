<template>
  <div class="addBucket right-side">
    <section class="content-header">
      <h1>
        Buckets添加
        <!--<small>Buckets</small>-->
      </h1>
      <ol class="breadcrumb">
        <li><router-link to="/admin"><i class="fa fa-dashboard"></i> 管理中心</router-link></li>
        <li><router-link to="/admin/bucket">Buckets</router-link></li>
        <li class="active">Buckets添加</li>
      </ol>
    </section>

    <!-- Main content -->
    <section class="content">

      <div class="row">
        <div class="col-md-12">
          <div class="box">
              <div class="box-header">
                <h3 class="box-title"></h3>
                <router-link to="/admin/addBucket">Buckets添加</router-link>
              </div>
              <!-- /.box-header -->
              <div class="box-body">
                <div class="form-horizontal">
                  <div class="form-group">
                    <label for="inputSubject">Bucket名称</label>
                    <input type="text" name="title" placeholder="标题" id="inputSubject" class="form-control">
                  </div>
                  <div class="form-group">
                    <label for="bucketKey">bucketKey</label>
                    <input type="text" name="bucketKey" id="bucketKey" class="form-control">
                  </div>
                  <div class="form-group">
                    <label for="buckettypes">buckettypes</label>
                    <input type="text" name="types" id="buckettypes" class="form-control">
                  </div>
                  <div class="form-group">
                    <label for="fluck">needFluck</label>
                    <input type="checkbox" name="needFluck" id="fluck" class="form-control">
                  </div>
                  <div class="box-footer clearfix">
                    <button class="btn btn-primary" type="submit" name="submit" value="publish">发布</button>
                    <button class="btn btn-info" type="submit" name="submit" value="save">仅保存</button>
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
  export default {
    name: 'AddBucket',
    data () {
      return {
        msg: 'Welcome to AddBucket'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
