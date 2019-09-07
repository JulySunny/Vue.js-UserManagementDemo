<template>
  <div class='add container'>
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">添加用户</h1>
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
        <button type="submit" class="btn btn-primary">添加</button>
      </div>
    </form>
  </div>
</template>

<script>
  import Alert from './Alert'
  export default {
    name: 'add',
    data () {
      return {
        customer:{},
        alert:""
      }
    },
    methods:{
      addCustomer(e){
        alert("ssss")
        /*阻止默认事件*/
        e.preventDefault()
        if (!this.customer.name || !this.customer.telephone || !this.customer.email){
          // console.log("请添加对应的信息")
          this.alert="请添加对应的信息"
        }else {
          let newCustomer={
            name:this.customer.name,
            telephone:this.customer.telephone,
            email:this.customer.email,
            education:this.customer.education,
            graducationschool:this.customer.graducationschool,
            profession:this.customer.profession,
            profile:this.customer.profile
          }
          this.$http.post("/api/user/save",newCustomer)
            .then(function (resp) {
              console.log(resp)
              /*添加完成后,跳转到主页里面去,传参数:query,在目标页面使用$router.query.alert去拿*/
              this.$router.push({path:'/',query:{alert:"用户信息添加 Success~~"}})
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
