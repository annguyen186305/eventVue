<template>
<div>
  <h1>{{textFormLogin}}</h1>
<!--  Count Click-->
  <h2> count: {{counter}} </h2>
  <button v-on:click="handleClick($event,5)">Click vao day</button>

<!--Mouse move-->
  <div class="box" v-on:mousemove="handleMouseMove">
            <p> ClientX: {{clientX}} </p>
            <p> ClientY: {{clientY}} </p>
    <div class="box-child" v-on:mousemove.stop="handleMouseMoveChild"> </div>
  </div>
<!-- Form Login -->
  <form action="./server.php" v-on:submit.prevent="handleSubmitForm">
    <label>Nhap userName</label>
    <input type="text" name="firstName" v-model="userName"/> <br>
    <label>Nhap password</label>
    <input type="text" name="passWord" v-model="passWord" /> <br>
    <button type="submit">Đăng Nhập</button>
  </form>

<!--Form tinh toan -->
<h3>{{textFormTinhToan}}</h3>
  <form>
<!--    {{nhapC}} <br>-->

    <label>Nhap A</label>
    <input type="number" name="A" v-model="a"/> <br>
    <label>Nhap B</label>
    <input type="number" name="B" v-model="b" /> <br>
<!--    <button type="submit">Tinh tong</button>-->
    <p>Tong moi</p>

    <input type="number" name="tongMoi" v-model="tongMoi" readonly/> <br>

    <p>Tong cu</p>

    <input type="number" name="tong" v-model="tong" readonly/> <br>
    <input type="number" name="hieu" v-model="hieu" readonly/> <br>
    <input type="number" name="nhan" v-model="nhan" readonly/> <br>
    <input type="number" name="chiaLayDu" v-model="chiaLayDu" readonly/> <br>
    <input type="number" name="chiaLayPhanNguyen" v-model="chiaLayPhanNguyen" readonly/> <br>
  </form>
  <button @click="changeActive"> Change Active</button>
  <div class="example" v-bind:class="objClass"></div>
  <p :class="thongBao">{{message}}</p>
</div>
</template>

<script>
export default {
  name: "countClick",
  props : {
    nhapC : Number,
  },
  data() {
    return{
      textFormLogin: 'Login Form',
      textFormTinhToan:'Form Tinh Toan',
      counter:0,
      clientX:0,
      clientY:0,
      userName:"",
      passWord:"",
      message: "",
      isActive : true,
      isError : false,
      status: "FAILED",
      a: 0,
      b: 0,
      tongMoi: 0
    }
  },
  methods:{
    handleClick(e, number){
      console.log('click', e);
      this.counter += number;
    },

    handleMouseMove(e){
      console.log('handleMouseMove', e.target);
      this.clientX = e.clientX;
      this.clientY = e.clientY;
    },
    handleMouseMoveChild(e){
      console.log('handleMouseMoveChild', e.target);
    },

    handleSubmitForm(e){
      console.log(e);
      console.log(this.userName);
      console.log(this.passWord);
      if(this.userName === "annguyen" && this.passWord === "123" ){
        this.color = "green";
        this.status = "SUCCESS";
        this.message = "Ban da dang nhap thanh cong"
      }
      else if (this.userName !== "annguyen" && this.passWord !== "123") {
        this.color = "red";
        this.status = "FAILED";
        this.message = "Ban da sai ca tai khoan va mat khau, vui long kiem tra lai"
      }
      else {
        this.color = "yellow";
        this.status = "WARNING";
        this.message = "Ban da sai ca tai khoan hoac mat khau, vui long kiem tra lai"
      }
        console.log(this.color, this.status, this.message);
    },
    changeActive(){
      this.isActive = !this.isActive
    }
  },
  watch: {
    // Theo doi su thay doi của các thuộc tính của component trong function và thực hiện 1 hành động nào đó
    // Theo doi a, neu a thay đổi thì thực thi function bên phải
    // nhapC: function () {
    //   this.tongMoi = Number(this.nhapC) + Number(this.b);
    //   console.log(this.nhapC)
    //   console.log("c thay doi , Tong moi = ", this.tongMoi)
    // },
    a: function () {
      this.tongMoi = Number(this.a) + Number(this.b);
      console.log("a thay doi , Tong moi = ", this.tongMoi)
    },
    b: function () {
      this.tongMoi = Number(this.a) + Number(this.b);
      console.log(this.a)
      console.log("b thay doi , Tong moi = ", this.tongMoi)
    },
    tong: function () {
      this.tongMoi = this.tong ;
      console.log("Tong thay doi , Tong moi = ", this.tongMoi)
    }
  },
  computed:{
    tong: function () {
      return Number(this.a) + Number(this.b);
    },
    hieu: function () {
      return Number(this.a) - Number(this.b);
    },
    nhan: function () {
      return Number(this.a) * Number(this.b);
    },
    chiaLayDu: function () {
      return Number(this.a) % Number(this.b);
    },
    chiaLayPhanNguyen: function () {
      return Number(this.a) / Number(this.b);
    },
    thongBao: function () {
      return {
        nenCam: this.status === "FAILED",
        red: this.status === "FAILED",
        green: this.status === "SUCCESS",
        nenXanh: this.status === "SUCCESS",
        yellow: this.status === "WARNING",
        gray: this.status === "WARNING",
      }
    },
    objClass : function () {
      return{
        active:this.isActive,
        error :this.isError
      }
    }
  }
}
</script>

<style scoped>
.box {
  width: 200px;
  height: 100px;
  position: relative;
  background-color: red;
}
.box-child {
  width: 50px;
  height: 50px;
  position: absolute;
  right: 0;
  top: 0;
  background-color: blue;
}
.example{
  width: 50px;
  height: 50px;
  background-color: yellowgreen;
}
.example.error{
  background-color: red;
}
.example.active{
  background-color: orange;
}

.red {
  color: red;
}


.green {
  color: green;
}

.yellow {
  color: yellow;
}

.nenCam {
  background-color: orange;
}

.nenXanh {
  background-color: #2c3e50;
}

.gray {
  background-color: grey;
}
</style>