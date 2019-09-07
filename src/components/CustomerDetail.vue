<template>
  <div class='customerdetail container'>
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      {{customer.name}}
      <span class="pull-right">
        <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
          编辑
        </router-link>
        <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">
          删除
        </button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="
glyphicon glyphicon-asterisk">{{customer.telephone}}</span></li>
      <li class="list-group-item"><span class="
glyphicon glyphicon-asterisk">{{customer.email}}</span></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'customerdetail',
    data () {
      return {
        customer: ''
      }
    },
    methods: {
      fetchCustomers (id) {
        this.$http.get('/api/user/findById/' + id).then(
          function (resp) {
            this.customer = resp.body
          })
      },
      deleteCustomer(id){
        console.log(id)
        this.$http.delete("/api/user/delete/"+id)
          .then(function (resp) {
            this.$router.push({path:"/",query:{alert:"用户删除成功"}})
          })
      }
    },
    created () {
      /*获取到传过来的id值==>>>具体看路由的那里*/
      this.fetchCustomers(this.$route.params.id)
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
