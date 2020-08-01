<template>
  <div style="position: relative; height: 100%">
    <div class=" container-fluid bg-light" >
      <div class="justify-content-center row header">
        <h1 class="display-4 text-light">Color Palette</h1>
      </div>
      <br>

      <!--    <p>{{this.colors}}</p>-->

      <div class="justify-content-center container-fluid">
        <button type="button" class="btn btn-block btn-dark button" data-toggle="modal" data-target="#add">
      <span>
        Add Color to Palette
      </span>
        </button>
      </div>

      <!-- The ADD Modal -->
      <div class="modal" id="add">
        <div class="modal-dialog">
          <div class="modal-content">

            <!-- Modal Header -->
            <div class="modal-header modal-header-design">
              <h4 class="modal-title">Add New Color</h4>
              <button type="button" class="close" data-dismiss="modal">&times;</button>
            </div>
            <!-- Modal body -->
            <div class="modal-body">
              <div class="row container">
                <form style="margin-right: 20px">
                  <div class="input-group">
                    <label>
                      <input type="color" style="width: 100px; height: 100px; padding: 0; border: none; background-color: #00000000" v-model="inputColor">
                    </label>
                  </div>
                </form>
                <div>
                  <h5>Please pick a Color</h5>
                  <label  style="text-shadow: 0px 0px 3px black"
                          :style="{color: this.inputColor}">{{ this.inputColor }}</label>
                </div>
              </div>
            </div>
            <!-- Modal footer -->
            <div class="modal-footer">
              <button type="button" class="btn btn-dark" @click="addColor()" data-dismiss="modal" >Done</button>
            </div>
          </div>
        </div>
      </div>

      <!-- The CHANGE Modal -->
      <div class="modal" id="change">
        <div class="modal-dialog">
          <div class="modal-content">

            <!-- Modal Header -->
            <div class="modal-header modal-header-design">
              <h4 class="modal-title">Change Color</h4>
              <button type="button" class="close" data-dismiss="modal">&times;</button>
            </div>
            <!-- Modal body -->
            <div class="modal-body">
              <div class="row container">
                <form style="margin-right: 20px">
                  <div class="input-group">
                    <label>
                      <input type="color" style="width: 100px; height: 100px; padding: 0; border: none; background-color: #00000000" v-model="inputColor">
                    </label>
                  </div>
                </form>
                <div>
                  <h5>Please pick a Color</h5>
                  <!--                <p>{{this.changingIndex}}</p>-->
                  <label  style="text-shadow: 0px 0px 3px black"
                          :style="{color: this.inputColor}">{{ this.inputColor }}</label>
                </div>
              </div>
            </div>
            <!-- Modal footer -->
            <div class="modal-footer">
              <!--            <button type="button" class="btn btn-dark" @click="changeColor()" >{{this.changingIndex}}|{{this.inputColor}}|Change</button>-->
              <button type="button" class="btn btn-dark" @click="changeColor()" data-dismiss="modal" >Change</button>
            </div>
          </div>
        </div>
      </div>

      <!--    <br>-->
      <br>
      <!--    <button @click="changeColor" class="btn btn-primary">change color</button>-->
      <!--    <div class="color" style="height: 100px; width: 100px; background-color: black"></div>-->
      <div class="">
        <ul class="list-group bg-dark palette " v-if="colors.length!==0" style="margin-bottom: 50px">
          <transition-group name="slide" type="in-out">
            <li class="list-group-item color "
                v-for="(color, index) in colors"
                :key="color"
                :style="{backgroundColor: colors[index]}"
            >
              <div  class="d-flex color-row">
                <div class="flex-grow-1">
                  <label class=" display-2 list-title">{{ color }}</label>
                </div>
                <button data-toggle="tooltip" data-placement="right" title="Remove Color" class="btn list-btn btn-sm" @click="removeColor(index)" style="margin-left: 10px"><i class="fa fa-trash"></i></button>
                <button data-toggle="tooltip" data-placement="right" title="Change Color" class="btn list-btn btn-sm" @click="setIndex(index)"><i class="fa fa-refresh" data-toggle="modal" data-target="#change"></i></button>
                <button data-toggle="tooltip" data-placement="right" title="Copy HEX" class="btn list-btn btn-sm" @click="copyColor(index)"><i class="fa fa-copy"></i></button>
              </div>

            </li>
          </transition-group>
        </ul>
      </div>
      <div class="justify-content-center row header" style=" bottom: 0">
        <a href="https://github.com/amir78729" target="_blank"><i class="fa fa-github" style="color: white"></i></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      colors: ['#e63946','#f1faee','#a8dadc','#457b9d','#1d3557'],
      hover: false,
      inputColor: '#6e6e6e',
      changingIndex: 0,
    }
  },
  methods: {
    changeColor () {
      // document.getElementsByClassName('h').style.backgroundColor = this.colors[index]
      this.colors.splice(this.changingIndex, 1, this.inputColor)
      // this.colors[this.changingIndex] = this.inputColor;
      // alert(this.colors[this.changingIndex])

    },
    addColor(color){
      this.colors.push(this.inputColor);
      // const pos = Math.floor(Math.random() * this.colors.length)
      // this.colors.splice(pos, 0, this.inputColor)
    },
    removeColor(index){
      this.colors.splice(index,1)
    },
    copyColor(index){
      const el = document.createElement('textarea')
      // Set value (string to be copied)
      el.value = this.colors[index]
      // Set non-editable to avoid focus and move outside of view
      el.setAttribute('readonly', '');
      el.style = {position: 'absolute', left: '-9999px'};
      document.body.appendChild(el);
      // Select text inside element
      el.select();
      // Copy text to clipboard
      document.execCommand('copy');
      // Remove temporary element
      document.body.removeChild(el);
    },
    setIndex(index){
      this.changingIndex = index;
    }
  }
}
</script>

<style>
  body{
    /*background-image: url("https://img.wallpapersafari.com/desktop/1920/1080/69/77/IRvbLk.jpg");*/
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-position: center;
    /*background-color : #222222;*/
  }
  .modal-header-design{
    background-image: url("https://img.wallpapersafari.com/desktop/1920/1080/94/3/Y7V4l0.jpg");
    color: white;
    border: none;
  }
  .header{
    background-image: url("https://img.wallpapersafari.com/desktop/1920/1080/94/3/Y7V4l0.jpg");
    box-shadow: 0 0 20px 0 #00000022 ;
  }
  .color {
    margin-bottom: 5px;

  }
  .color button{
    /*height: 0;*/
    opacity: 0;
    transition: all .5s;
  }
  .color:hover button{
    /*height: auto;*/
    opacity: 1;
    transition: all .5s;
  }
  .color:hover{
    /*box-shadow: 10px 0px 20px 20px #00000033 inset;*/
  }
  .color label{
    /*height: auto;*/
    min-width: 180px;
    text-align: center;
    opacity: 0.2;
    height: 40px;
    width: 20%;
    transition:  0.5s ;
  }
  .color:hover label{
    /*height: auto;*/
    opacity: 1;
    border-radius: 20px;
    width: 100%;
    transition:  0.5s ;
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
  .color-row{
    height: auto;
    transition: height 0.5s;
  }
  .color-row:hover{
    height: auto;
    transition: height 0.5s;
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
    transition: transform 1s ease-out;
  }
  .list-title{
    font-family: Consolas;
    background-color: #00000077;
    border-radius: 5px;
    padding: 4px 12px;
    /*height: 100%;*/
    color: white;
    font-size: 25px;
    /*text-align-all: center;*/
  }
  .list-btn{
    height: 40px;
    width: 40px;
    border-radius: 50%;
  }
  .hr-text {
    line-height: 1em;
    position: relative;
    outline: 0;
    border: 0;
    color: black;
    text-align: center;
    height: 1.5em;
    opacity: .5;


  }
  .button {
    /*border-radius: 4px;*/
    /*background-color: #f4511e;*/
    /*border: none;*/
    /*color: #FFFFFF;*/
    text-align: center;
    /*font-size: 28px;*/
    /*padding: 20px;*/
    /*width: 200px;*/
    transition: all 0.5s;
    cursor: pointer;
    margin: 5px;
  }

  .button span {
    cursor: pointer;
    display: inline-block;
    position: relative;
    transition: 0.5s;
  }

  .button span:after {
    content: '+';
    position: absolute;
    opacity: 0;
    top: 0;
    right: -20px;
    transition: 0.5s;
    color: #42b983;
    font-weight: bolder;
  }

  .button:hover span {
    padding-right: 25px;
  }

  .button:hover span:after {
    opacity: 1;
    right: 0;
  }
</style>
