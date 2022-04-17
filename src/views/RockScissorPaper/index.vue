<template>
  <div class="wrapper">
      <div class="container">
          <div class="computer-choice">Computer Choice: {{computerChoice}}</div>
          <div class="PK">PK</div>
          <div class="user-choice">
            User Choice: {{userChoice}}
            <div class="button">
              <el-button type="primary" size="small"  @click="handleChoice">rock</el-button>
              <el-button type="warning" size="small"  @click="handleChoice">scissor</el-button>
              <el-button type="success" size="small"  @click="handleChoice">paper</el-button>
            </div>
          </div>
          
      </div>
      
  </div>
</template>

<script setup>
import { ElButton, ElMessage, ElMessageBox } from 'element-plus'

import { ref } from "@vue/reactivity";

let computerChoice = ref('')
let userChoice = ref('')
let result = ref('')

const handleChoice = (e) => {
  userChoice.value = e.target.innerText
  generateComputerChoice()
  getResult()
}
const generateComputerChoice = () => {
  const randomNumber = Math.floor(Math.random() *3 ) +1;
  const computerChoiceObj = {
    1: 'rock',
    2: 'scissor',
    3: 'paper'
  }
  computerChoice.value = computerChoiceObj[randomNumber]
  console.log('computerChoice',computerChoice);
}
const getResult = () => {
  if (computerChoice.value === userChoice.value) {
    result.value = 'Its a draw!'
  }
  if (
      userChoice.value === 'rock' && computerChoice.value === 'scissor' 
      || userChoice.value === 'scissor' && computerChoice.value === 'paper'
      || userChoice.value === 'paper' && computerChoice.value === 'rock'
  ) {
      result.value = 'Congratulations!  You win!'
    }
  if (
      userChoice.value === 'rock' && computerChoice.value === 'paper' 
      || userChoice.value === 'scissor' && computerChoice.value === 'rock' 
      || userChoice.value === 'paper' && computerChoice.value === 'scissor'
  ) {
      result.value = 'Uh, You lost!'
  }
  setTimeout(() => ElMessageBox.alert(result.value), 500)
}
</script>

<style lang="scss">
  .wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background-image: url('./background.png');
    background-repeat:no-repeat;
    background-size: 100% 100%;
  }
  .container {
    display: flex;
    align-items: center;
    width: 700px;
    height: 500px;
    background-color: #fff;
    .computer-choice, .PK, .user-choice {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    .button {
      margin-top: 10px;
    }
    .PK {
      font-size: 60px;
      color: orange;
      font-family: fantasy;
    }

  }
</style>