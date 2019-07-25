<template>
  <div class="hello">
    <el-carousel :interval="4000" type="card" width="300px" height="200px" autoplay=true>
      <el-carousel-item v-for="item in imagesbox" :key="item.id">
      <img :src = "item.idView" class = "image"> 
      <h3 class="medium">{{ item }}</h3>
      </el-carousel-item>
    </el-carousel>

    <el-divider></el-divider>
    
    <!--登录界面-->
    <form v-if="!isReg">
      <el-input v-model="name" placeholder="用户名" style = "width: 300px;"></el-input><br>
      <el-input placeholder="密码" v-model="password" show-password style = "width: 300px;"></el-input><br>
      <el-button @click="reg()" class = "log">注册</el-button>
      <el-button type = "primary" @click="login()" class = "log">登录</el-button>
    </form>
    
    <!--注册界面-->
    <form v-else>
      <el-input v-model="name" placeholder="用户名" style = "width: 300px;"></el-input><br>
      <el-input placeholder="密码" v-model="password" show-password style = "width: 300px;"></el-input><br>
      <el-input v-model="repeat" placeholder="确认密码" show-password style = "width: 300px;"></el-input><br>
      <el-button @click="addUser()">确定</el-button>
      <el-button type = "primary" @click="cancel()">取消</el-button>
    </form>
  </div>
</template>

<style>
  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }

</style>

<script>
  export default {
      data() {
        return {
          isReg: false,
          name: '',
          password: '',
          repeat: '',
          imagesbox:[{id:0,idView:require("../assets/images/dog1.jpg")},
                     {id:1,idView:require("../assets/images/dog2.jpg")},
                     {id:2,idView:require("../assets/images/dog3.jpg")},
                     {id:3,idView:require("../assets/images/dog4.jpg")},
                     {id:4,idView:require("../assets/images/dog5.jpg")},
                     {id:5,idView:require("../assets/images/dog6.jpg")}],
      
      }
    },

    methods: {
      login() {
        if(
          (localStorage.getItem("name") === this.name) &&
          (localStorage.getItem("password") === this.password)
        ){
            this.name = "";
            this.password = "";
            this.$router.push("page1");
        }else{
          alert("用户名或密码不正确！");
        }
       
      },

      reg() {
        this.isReg = true;
      },

      cancel() {
        this.isReg = false;
      },

      addUser() {
        if(this.password === this.repeat){
          localStorage.setItem("name", this.name);
          localStorage.setItem("password", this.password);

          this.name = "";
          this.password = "";
          this.repeat = "";
          this.isReg = false;
          alert("注册成功！");
        }else{
          alert("两次密码不一致！");
        }
      }
    },

    mounted() {

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
