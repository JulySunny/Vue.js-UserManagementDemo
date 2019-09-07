<template>
  <div class='customer container'>
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
    <!--搜索功能-->
    <input type="text" class="form-control" placeholder="搜索" v-model="filterInput"><br>
    <table class="table table-striped">
      <thead>
      <tr>
        <th>姓名</th>
        <th>电话</th>
        <th>邮箱</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(customer,index) in filterBy(customers,filterInput)" :key="index">
        <th>{{customer.name}}</th>
        <th>{{customer.telephone}}</th>
        <th>{{customer.email}}</th>
        <!--注意: 如果绑定表达式,则需要使用v-bind:to ,如果全是纯字符串的话,就可以使用to-->
        <td>
          <router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link>
        </td>
        <th></th>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert'

  export default {
    name: 'customer',
    data () {
      return {
        customers: [],
        alert: '',
        filterInput:""
      }
    },
    methods: {
      /*
      Note:
      搜索功能的实现
      * */
      filterBy (customers,value) {
        /*filter是Es6的方法,会遍历整个数组*/
        return customers.filter(function (customer) {
        /*match是Es6的方法,匹配value*/
          return customer.name.match(value)
        })
      },
      fetchCustomers () {
        this.$http.get('/api/user/findAll').then(
          function (resp) {
            this.customers = resp.body
          })
      }
    },
    created () {
      if (this.$route.query.alert) {
        /*判断是否添加成功*/
        this.alert = this.$route.query.alert
      }
      this.fetchCustomers()
    },
    components: {
      // 注册组件,ES6语法
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
