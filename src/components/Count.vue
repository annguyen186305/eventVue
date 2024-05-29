<template>
<div>
  <h1> count: {{counter}} </h1>
  <button v-on:click="handleClick($event,5)">Click vao day</button>
  <div class="box" v-on:mousemove="handleMouseMove">
            <p> ClientX: {{clientX}} </p>
            <p> ClientY: {{clientY}} </p>
    <div class="box-child" v-on:mousemove.stop="handleMouseMoveChild"> </div>
  </div>
  <form action="" v-on:submit.prevent="handleSubmitForm">
    <label>Nhap firstName</label>
    <input type="text" name="firstName"> <br>
    <label>Nhap email</label>
    <input type="email" name="email"> <br>
    <input type="submit" value="dang nhap">
  </form>
</div>
</template>

<script>
export default {
  name: "countClick",
  data() {
    return{
      counter:0,
      clientX:0,
      clientY:0
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
    handleSubmitForm(e){
      console.log(e);
    },
    handleMouseMoveChild(e){
      console.log('handleMouseMoveChild', e.target);
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
</style>