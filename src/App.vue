<template>
  <div class=" container bg-light">
    <div class="row">
      <form>
<!--        <div class="input-group">-->
<!--          <div class="input-group-prepend">-->
<!--            <div class="input-group-text" style="width: 120px">{{inputColor}}</div>-->
<!--          </div>-->
<!--          <input type="color" class="form-control" id="inlineFormInputGroupUsername" placeholder="color" v-model="inputColor">-->
<!--        </div>-->
        <div class="input-group">
          <input type="color" style="width: 50px; height: 50px; padding: 0; border: none; background-color: #00000000" v-model="inputColor">
        </div>
      </form>
      <button @click="addColor" class="btn btn-dark">add color</button>

    </div>
<!--    <p>#{{inputColor}}</p>-->
    <br>
    <button @click="changeColor" class="btn btn-primary">change color</button>
    <div class="color" style="height: 100px; width: 100px; background-color: black"></div>
    <ul class="list-group bg-dark" style="padding: 5px; border-radius: 10px">
      <li class="list-group-item color d-flex" v-for="(c, index) in colors" >
        <label class="flex-grow-1">{{ c }}</label>
        <button class="btn list-btn btn-sm" @click="removeColor(index)">remove color</button>
        <button class="btn list-btn btn-sm" @click="removeColor(index)">change color</button>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  data () {
    return {
      colors: ['#FFEE00'],
      inputColor: 'select:',
    }
  },
  methods: {
    changeColor (index) {
      alert(index)
      document.getElementsByClassName('h').style.backgroundColor = this.colors[index]
    },
    addColor(){
      this.colors.push(this.inputColor);
    },
    removeColor(index){
      this.colors.splice(index,1)
    }
  }
}
</script>

<style>
  .color {
    background-color: #42b983;
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
</style>
