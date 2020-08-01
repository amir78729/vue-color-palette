<template>
  <div class=" container-fluid bg-light">
    <div class="justify-content-center row header">
      <h1 class="display-4 text-light">Color Palette</h1>
    </div>
    <div class="row">
      <form>
        <div class="input-group">
          <label>
            <input type="color" style="width: 50px; height: 50px; padding: 0; border: none; background-color: #00000000" v-model="inputColor">
          </label>
        </div>
      </form>
      <button @click="addColor" class="btn btn-dark">add color</button>
    </div>

    <br>
<!--    <button @click="changeColor" class="btn btn-primary">change color</button>-->
<!--    <div class="color" style="height: 100px; width: 100px; background-color: black"></div>-->
    <ul class="list-group bg-dark palette">
      <transition-group name="slide" type="in-out">
        <li class="list-group-item color "
            v-for="(color, index) in colors"
            :key="color"
            :style="{backgroundColor: colors[index]}"
            >
          <div  class="d-flex">
            <div class="flex-grow-1">
              <label class="list-title">{{ color }}</label>
            </div>
              <button class="btn list-btn btn-sm" @click="removeColor(index)"><i class="fa fa-trash"></i></button>
              <button class="btn list-btn btn-sm" @click="changeColor(index)"><i class="fa fa-refresh"></i></button>
              <button class="btn list-btn btn-sm" @click="copyColor(index)"><i class="fa fa-copy"></i></button>
<!--            <button class="btn list-btn btn-sm" @click="removeColor(index)">remove color</button>-->
<!--            <button class="btn list-btn btn-sm" @click="changeColor(index)">change color</button>-->
<!--            <button class="btn list-btn btn-sm" @click="copyColor(index)">copy hex</button>-->
          </div>

        </li>
      </transition-group>
    </ul>

  </div>
</template>

<script>
export default {
  data () {
    return {
      colors: ['#FFEE00','#123123','#456456','#756765','#3215ac','#123346','#765345'],
      hover: false,
      inputColor: 'select:',
    }
  },
  methods: {
    changeColor (index) {
      alert(index)
      document.getElementsByClassName('h').style.backgroundColor = this.colors[index]
    },
    addColor(color){
      this.colors.push(this.inputColor);
      // const pos = Math.floor(Math.random() * this.colors.length)
      // this.colors.splice(pos, 0, this.inputColor)
    },
    removeColor(index){
      this.colors.splice(index,1)
    }
  }
}
</script>

<style>
  .header{
    background-image: url("https://wallup.net/wp-content/uploads/2018/09/25/629276-abstract-colorful.jpg");

  }
  .color {
    margin-bottom: 5px;

  }
  .color button{
    /*height: 0;*/
    opacity: 0;
    transition: all .2s;
  }
  .color:hover button{
    /*height: auto;*/
    opacity: 1;
    transition: all .2s;
  }
  .color button{
    margin: 0 5px;
    background-color: #00000077;
    color: white;
  }
  .color button:hover{
    background-color: #00000099;
    color: white;
  }
  .slide-enter{
    opacity: 0;
  }
  .slide-enter-active{
    animation: slide-in 1s ease-out forwards;
    transition: opacity 1s;
    /*position: absolute;*/
  }
  .slide-leave{

  }
  .slide-leave-active{
    animation: slide-out 1s ease-out forwards;
    transition: opacity 0s;
    opacity: 0;
    position: absolute;
  }
  .slide-move{
    transition: transform 1s;
  }
  @keyframes slide-in {
    from{
      transform: translateY(-20px);
    }
    to{
      transform: translateY(0px);
    }
  }
  @keyframes slide-out {
    from{
      transform: translateY(0px);
    }
    to{
      transform: translateY(-20px);
    }
  }
  .palette {
    padding: 5px;
    border-radius: 10px;
    transition: transform 1s;
  }
  .list-title{
    background-color: #00000077;
    border-radius: 5px;
    padding: 4px 12px;
    color: white;
  }
  .list-btn{
    height: 50px;
    width: 50px;
    border-radius: 50%;
  }
</style>
