<template>
  <div class=" details  container">
    <router-link to="/" class="btn btn-default">返回</router-link>
  <h1 class="page-header">
    {{cus.name}}

    <span class="pull-right">
      <router-link class="btn btn-primary" v-bind:to="'/edit/'+cus.id">
        编辑
      </router-link>
      <button class="btn btn-danger" v-on:click="deleteCus(cus.id)">删除</button>
    </span>
  </h1>
  <ul class="list-group">
    <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">  {{cus.phone}}</span></li>
    <li class="list-group-item"><span class="glyphicon glyphicon-plus">  {{cus.email}}</span></li>
  </ul>
  <ul class="list-group">
    <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">  {{cus.education}}</span></li>
    <li class="list-group-item"><span class="glyphicon glyphicon-plus">  {{cus.profession}}</span></li>
  </ul>
  <ul class="list-group">

    <li class="list-group-item"><span class="glyphicon glyphicon-plus">  {{cus.profile}}</span></li>
  </ul>
  </div>

</template>

<script>
export default {
  name: 'cusdetail',
  data () {
    return {
      cus: ''
    }
  },
  methods: {
    fetchCustomers (id) {
      this.$http.get('http://localhost:3000/users/' + id)
        .then(function (response) {
          console.log(response)
          this.cus = response.body
        })
    },

    deleteCus (id) {
      // console.log(id);
      this.$http.delete('http://localhost:3000/users/' + id)
        .then(function (response) {
          this.$router.push({path: '/', query: {alert: '用户删除成功！'}})
        })
    }
  },
  created () {
    this.fetchCustomers(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
