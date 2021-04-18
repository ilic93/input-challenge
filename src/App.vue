<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <header>
      <h1>Input Gallery</h1>
      <p>Choose your input field or create one yourself</p>
    </header>
    <main>
      <div>
        <InputComp :customButton="true"/>
      </div>
      <div @mousemove="checkInput()">
        <code class="galleryCode">&lt;Input /&gt;</code>
        <InputComp class="moveLeft default"/>
      </div>
      <div>
        <code class="galleryCode">&lt;Input error /&gt;</code>
        <InputComp class="moveLeft errorInput" :errorLength="100"/>
      </div>
      <div>
        <code class="galleryCode">&lt;Input disabled /&gt;</code>
        <InputComp class="moveLeft" :disabledInput="true"/>
      </div>
      <div class="inputWithHelpText">
        <div>
          <code class="galleryCode">&lt;Input helperText="Some interesting text" /&gt;</code>
          <InputComp class="default" :interestingTxt="'Some interesting text'"/>
        </div>
        <div>
          <code class="galleryCode">&lt;Input helperText="Some interesting text" error /&gt;</code>
          <InputComp class="errorInput" :interestingTxt="'Some interesting text'" :errorLength="100"/>
        </div>
      </div>
      <div class="inputWithIcons">
        <div>
          <code class="galleryCode">&lt;Input startIcon /&gt;</code>
          <InputComp class="default leftIcon" :startIcon="true" />
        </div>
        <div>
          <code class="galleryCode">&lt;Input endIcon /&gt;</code>
          <InputComp class="default" :endIcon="true" />
        </div>
      </div>
      <div>
        <code class="galleryCode">&lt;Input value="text" /&gt;</code>
        <InputComp class="moveLeft default" :definedValue="'Text'" />
      </div>
      <div class="inputWithSizes">
        <div>
          <code class="galleryCode">&lt;Input size="sm" /&gt;</code>
          <InputComp class="default" :definedSize="'sm'" />
        </div>
        <div>
          <code class="galleryCode">&lt;Input size="md" /&gt;</code>
          <InputComp class="default" />
        </div>
        <div>
          <code class="galleryCode">&lt;Input size="lg" /&gt;</code>
          <InputComp class="default" :definedSize="'lg'" />
        </div>
      </div>
      <div>
        <code class="galleryCode">&lt;Input fullWidth /&gt;</code>
        <InputComp class="moveLeft default fullWidthInput"/>
      </div>
      <div>
        <code class="galleryCode">&lt;Input multiline row="4" /&gt;</code>
        <InputComp class="moveLeft default multiline" :defaultTextarea="true" />
      </div>
    </main>
    <footer>Author: Marko Ilic</footer>
  </div>
</template>

<script>
import InputComp from './components/InputComp.vue'

export default {
  name: 'App',
  components: {
    InputComp
  },
  methods: {
    checkInput() {
      const x = document.querySelector('.default input')
      if(x == document.activeElement) {
        document.querySelector('.default code').style.color = 'blue'
      } else if(x.matches(':hover')) {
        document.querySelector('.default code').style.color = 'black'
      } 
      else {
        document.querySelector('.default code').style.color = 'grey'
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 10px;
}

header {
  margin-bottom: 15px;
}

main > div, .inputWithHelpText > div, .inputWithIcons > div {overflow: hidden;}

.inputWithHelpText > div,
.inputWithIcons > div {
  float: left; 
  margin-right: 10px; 
  width: 45%;
}

.inputWithHelpText > div > code.galleryCode, .inputWithIcons > div > code.galleryCode, .inputWithSizes > div > code.galleryCode {width: 100%;}
.inputWithHelpText .inputDiv, .inputWithIcons .inputDiv, .inputWithSizes .inputDiv  {float: left;}

.inputWithSizes > div {
  float: left; 
  margin-right: 10px; 
  width: 30%;
}

.galleryCode {
  margin: 15px 0; 
  font-size: 14px;
}

.moveLeft {
  float: left;
}

.errorInput input {border-color: red;}
.errorInput input:hover {border-color: black !important;}
.errorInput code, .errorInput .ht {color: red;}

.default:hover code, .default:hover .ht,
.errorInput:hover code, .errorInput:hover .ht {
  color: black;
}

.leftIcon input {padding-left: 40px;}

.fullWidthInput, .fullWidthInput .subInputDiv, .fullWidthInput code {width: 100%;}
.fullWidthInput input {width: 95%;}

.multiline input {display: none;}
</style>
