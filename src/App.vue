<template>
  <div class=" container bg-light">
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
        <li class="list-group-item color d-flex"
            v-for="(color, index) in colors"
            :key="color"
            :style="{backgroundColor: colors[index]}">
          <div class="flex-grow-1">
            <label class="display-5">{{ color }}</label>
          </div>

          <button class="btn list-btn btn-sm" @click="removeColor(index)">remove color</button>
          <button class="btn list-btn btn-sm" @click="removeColor(index)">change color</button>

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
  .color {
    margin-bottom: 5px;
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
    transition: opacity 0.5s;
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
</style>
