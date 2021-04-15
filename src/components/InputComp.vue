<template>
  <div>
    <div class="inputDiv">
      <code>Label</code>
      <div class="subInputDiv">
        <input name="inputField" type="text" placeholder="Placeholder" 
        :minlength="errorLength || 5" 
        :class="definedSize || 'md'" 
        :disabled="disabledInput" 
        :value="definedValue"
        />
        <textarea v-if="showTextarea || defaultTextarea" placeholder="Write something..." minlength="5" rows="4"></textarea>
        <span v-if=" startIcon || showLeftIcon && !showTextarea" class="material-icons left">{{ newLeftIcon || 'call made'}}</span>
        <span v-if=" endIcon || showRightIcon && !showTextarea" class="material-icons right">{{ newRightIcon || 'call made'}}</span>
      </div>
      <p class="ht">{{ interestingTxt || helpText }}</p>
    </div>
    <button v-if="customButton" @click="toggleForm()">Customaze input</button>
    <form v-if="activeForm" name="inputForm" @submit.prevent="updateInput()">
      <label>Disable input: </label>
      <input type="checkbox" name="disableCheck"/> 
      <hr>
      <label>Enter helper text:</label>
      <input type="text" v-model="helpText" maxlength="30"/>
      <hr>
      <label>Icons:</label><br>
      <input type="checkbox" name="leftIcon" value="true"/> Left
      <select name="leftIconSelect">
        <option value="call made">call icon</option>
        <option value="list">list icon</option>
        <option value="label">label icon</option>
        <option value="send">send icon</option>
        <option value="launch">launch icon</option>
      </select><br>
      <input type="checkbox" name="rightIcon" value="true"/> Right
      <select name="rightIconSelect">
        <option value="call made">call icon</option>
        <option value="list">list icon</option>
        <option value="label">label icon</option>
        <option value="send">send icon</option>
        <option value="launch">launch icon</option>
      </select>
      <hr>
      <label>Size:</label>
      <select name="sizeSelection">
        <option value="sm">small</option>
        <option value="md" selected>middle</option>
        <option value="lg">large</option>
      </select>
      <hr>
      <label>Full width input:</label>
      <input type="checkbox" name="fullWidth" value="true"/>
      <hr>
      <label>Input color:</label>
      <input type="color" name="inputColor" value="#808080"/>
      <hr>
      <label>Multiline input:</label>
      <input type="checkbox" name="multilineInput" value="true"/>
      <hr>
      <label>Apply changes:</label>
      <input type="submit" value="apply">
      
    </form>
  </div>
</template>

<script>
export default {
  props: ['customButton', 'errorLength', 'disabledInput', 'interestingTxt', 'startIcon', 'endIcon', 'definedValue', 'definedSize', 'defaultTextarea'],
  data() {
    return {
      activeForm: false,
      helpText: '',
      showLeftIcon: false,
      showRightIcon: false,
      showFullWidth: false,
      showTextarea: false,
      newLeftIcon: '',
      newRightIcon: '',
      }
  },
  methods: {
    toggleForm() {
      this.activeForm = !this.activeForm
    },
    updateInput() {
      const inputField = document.querySelector('input[name="inputField"]')
      const textareaField = document.querySelector('textarea')

      if(document.inputForm.disableCheck.checked) {
        inputField.setAttribute('disabled', 'true')
        if(textareaField) textareaField.setAttribute('disabled', 'true')
      } else {
        inputField.removeAttribute('disabled')
        if(textareaField) textareaField.removeAttribute('disabled')
      }
    
      this.showLeftIcon = document.inputForm.leftIcon.checked
      this.showRightIcon = document.inputForm.rightIcon.checked
      this.showFullWidth = document.inputForm.fullWidth.checked
      this.showTextarea = document.inputForm.multilineInput.checked

      if(this.showLeftIcon) {
        inputField.classList.add('inputWithLeftIcon')
      } else {
        inputField.classList.remove('inputWithLeftIcon')
      }

      if(this.showFullWidth && !this.showTextarea) {
        inputField.classList.add('fullWidth')
        document.querySelector('.subInputDiv').classList.add('subInputDivFull')
        document.querySelector('code').style.width = '90%'
      } else {
        inputField.classList.remove('fullWidth')
        document.querySelector('.subInputDiv').classList.remove('subInputDivFull')
        document.querySelector('code').style.width = '240px'
      }

      this.newLeftIcon = document.querySelector('select[name="leftIconSelect"]').value
      this.newRightIcon = document.querySelector('select[name="rightIconSelect"]').value

      let sizes = ['sm', 'md', 'lg']
      const newSize = document.querySelector('select[name="sizeSelection"]').value
      const index = sizes.indexOf(newSize)
      sizes.splice(index, 1)
      inputField.classList.add(newSize)
      inputField.classList.remove(...sizes)

      const newColor = document.inputForm.inputColor.value
      inputField.style.borderColor = newColor
      document.querySelector('code').style.color = newColor
      document.querySelector('.ht').style.color = newColor

      if(this.showTextarea) {
        inputField.style.display = 'none'
      } else {
        inputField.style.display = 'inline-block'
      }
    }
  }
  
}
</script>

<style> 
 input, textarea {
   border: 1px solid grey;
   border-radius: 8px;
   padding-left: 10px;
 }

 input:hover, textarea:hover {border-color: black !important; cursor: pointer;}
 input:focus, textarea:focus {border-color: blue !important; outline: 0; cursor: wait;}
 input:invalid, textarea:invalid {border-color: red !important; box-shadow: none;}
 input:disabled {cursor: not-allowed;} 

 form {text-align: left; margin: 15px 35%; padding: 10px 5px; border: 3px solid lightblue; border-radius: 10px; }
 label {margin-right: 10px;}
 
 .sm {
   height: 2em;
 }

 .md {
   height: 4em;
 }

 .lg {
   height: 6em;
 }
 
 code {display: block; font-size: 16px;}
 .ht {font-size: 14px;}

 .ht, code, .subInputDiv, textarea {
   width: 240px;
   margin: 0 auto;
   text-align: left;
 }

 .inputDiv {
   margin-bottom: 15px;
 }

 .material-icons.left {position: absolute; left: 10px; width: 24px;}
 .material-icons.right {position: absolute; width: 24px; right: 10px;}

 .md ~ .material-icons.left, .md ~ .material-icons.right {padding: 19px 0;}
 .sm ~ .material-icons.left, .sm ~ .material-icons.right {padding: 4px 0;}
 .lg ~ .material-icons.left, .lg ~ .material-icons.right  {padding: 34px 0;}

 .subInputDiv {position: relative; display: inline-block;}

 .inputWithLeftIcon {
   padding-left: 40px;
 }

 .fullWidth {
   width: 100%;
 }

 .subInputDivFull {
   width: 90%;
 }

 .subInputDivFull ~ .ht, .subInputDivFull ~ code {width: 90%;}
 
</style>