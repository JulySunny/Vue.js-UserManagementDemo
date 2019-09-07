<template>
  <div class='edit container'>
    <!--
    Note:
      父子组件交互逻辑说明
      首先是两个组件:Alert和编辑页两个组件
      编辑页面里面使用message属性给Alert组件传值,Alert组件使用props:[message]接收父组件的值
      传递的信息就是alert对象"请添加对应的用户信息"
    -->
    <Alert v-bind:message="alert"></Alert>
    <h1 class="page-header">编辑用户</h1>
    <form v-on:submit="addCustomer">
      <div class="well">
        <h4>用户信息</h4>
        <!--姓名-->
        <div class="form-group">
          <label>姓名</label>
          <input type="text" class="form-control" placeholder="name" v-model="customer.name">
        </div>
        <!--电话-->
        <div class="form-group">
          <label>电话</label>
          <input type="text" class="form-control" placeholder="telephone" v-model="customer.telephone">
        </div>
        <!--邮箱-->
        <div class="form-group">
          <label>邮箱</label>
          <input type="text" class="form-control" placeholder="email" v-model="customer.email">
        </div>
        <!---->
        <div class="form-group">
          <label>学历</label>
          <input type="text" class="form-control" placeholder="education" v-model="customer.education">
        </div>
        <!---->
        <div class="form-group">
          <label>毕业学校</label>
          <input type="text" class="form-control" placeholder="graduationschool" v-model="customer.graduationschool">
        </div>
        <!---->
        <div class="form-group">
          <label>职业</label>
          <input type="text" class="form-control" placeholder="profession" v-model="customer.profession">
        </div>
        <!---->
        <div class="form-group">
          <label>个人简介</label>
          <br/>
          <!--<input type="text" class="form-control" placeholder="" v-model="customer.profile">-->
          <textarea name="form-control"  cols="135" v-model="customer.profile" rows="10"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">确认</button>
      </div>
    </form>
  </div>
</template>

<script>
  import Alert from './Alert'
  export default {
    name: 'edit',
    data () {
      return {
        customer:{},
        alert: ""
      }
    },
    created(){
      this.fetchCustomer(this.$route.params.id)
    },
    methods:{
      fetchCustomer(id){
        this.$http.get("/api/user/findById/"+id)
          .then(function (resp) {
            this.customer=resp.body
          })
      },
      addCustomer(e){
        alert("ssss")
        /*
        Note:
        阻止默认事件e.preventDefault(),用来阻止默认的表单提交事件
        */
        e.preventDefault()
        if (!this.customer.name || !this.customer.telephone || !this.customer.email){
          // console.log("请添加对应的信息")
          this.alert="请添加对应的信息"
        }else {
          /*
          Note:
          * let 关键字定义的变量 是"块级别的作用的范围"
          * var 关键字定义的变量 是"全局级别的作用范围"
          * */
          let updateCustomer={
            name:this.customer.name,
            telephone:this.customer.telephone,
            email:this.customer.email,
            education:this.customer.education,
            graducationschool:this.customer.graducationschool,
            profession:this.customer.profession,
            profile:this.customer.profile
          }
          /*
          Note:
          * 这里的id是来自于==>>点击编辑按钮的时候,传递过来的Id
          * ,因此可以通过route路由拿到这个数据
          * 注意:跳转路由是this.$router.push({path:'/',query:{k:V}})
          *      获取路由传递过来的参数是 this.$route.params.key ,少了一个route
          * */
          this.$http.put("/api/user/update/"+this.$route.params.id,updateCustomer)
            .then(function (resp) {
              console.log(resp)
              /*
              Note:
              *添加完成后,跳转到主页里面去,传参数:query,
              *在目标页面使用$route.query.alert去拿
              */
              this.$router.push({path:'/',query:{alert:"用户信息更新 Success~~"}})
            })
          e.preventDefault()
        }
        e.preventDefault()
      }
    },
    components:{
      Alert
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

