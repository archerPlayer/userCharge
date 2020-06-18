<template>
  <div class=" add  container">
    <Alert v-if="alert" v-bind:message = "alert"></Alert>
  <h1 class="page-header">添加用户</h1>
  <form v-on:submit = "addCustomer">
<div class="well">
<h4>用户信息</h4>
<div class="form-group">
  <label>姓名</label>
  <input type = "text" class="form-control" placeholder="name" v-model = "cus.name">
</div>
<div class="form-group">
  <label>电话</label>
  <input type = "text" class="form-control" placeholder="phone" v-model = "cus.phone">
</div>
<div class="form-group">
  <label>邮箱</label>
  <input type = "text" class="form-control" placeholder="email" v-model = "cus.email">
</div>
<div class="form-group">
  <label>学历</label>
  <input type = "text" class="form-control" placeholder="education" v-model = "cus.education">
</div>
<div class="form-group">
  <label>职业</label>
  <input type = "text" class="form-control" placeholder="profession" v-model = "cus.profession">
</div>
<div class="form-group">
  <label>个人简介</label>
<textarea class="form-controol" rows="10" v-model="cus.profile"></textarea>
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
      cus:{},
      alert:""
    }
  },
  methods:{
    addCustomer(e){
      //console.log(123);
    if(!this.cus.name || !this.cus.phone || !this.cus.email){
    //  console.looog("请添加对应的信息");
    this.alert = "请添加对应的信息";
    }else{
      let newCustomer = {
        name:this.cus.name,
        phone:this.cus.phone,
        email:this.cus.email,
        education:this.cus.education,
        profession:this.cus.profession,
        profile:this.cus.profile
      }
      this.$http.post("http://localhost:3000/users",newCustomer)
      .then(function(response){
        //coonsole.log(response);
      this.$router.push({path:"/",query:{alert:"用户信息添加成功！"}});
      })
        e.preventDefault();
    }
      e.preventDefault();
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
