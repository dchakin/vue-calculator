<template>
  <div class="container">
    <div class="topbar">
      <div class="topbar__toggle">
        <i class="ri-menu-3-line"></i>
      </div>
      <div class="topbar__theme">
        <i @click="changeTheme" class="ri-moon-line" id="theme-button"></i>
      </div>
    </div>

    <div class="panel">
      <div class="panel__back">
        <p id="panel__back">0</p>
      </div>
      <div class="panel__main">
        <input placeholder="0" v-model="result" class="panel__main-input" id="input" type="text">
      </div>
    </div>

    <div class="num">
      <div class="num__grid">
        <button @click="input('reset')" class="num__grid-item">CE</button>
        <button @click="input('back')" class="num__grid-item">
          <i class="ri-delete-back-2-line"></i>
        </button>
        <button @click="input('/')" class="num__grid-item">/</button>
        <button @click="input('*')" class="num__grid-item">*</button>

        <button @click="input(7)" class="num__grid-item">7</button>
        <button @click="input(8)" class="num__grid-item">8</button>
        <button @click="input(9)" class="num__grid-item">9</button>
        <button @click="input('-')" class="num__grid-item">-</button>

        <button @click="input(4)" class="num__grid-item">4</button>
        <button @click="input(5)" class="num__grid-item">5</button>
        <button @click="input(6)" class="num__grid-item">6</button>
        <button @click="input('+')" class="num__grid-item">+</button>
      </div>

      <div class="num__grid-second">
        <button @click="input(1)" class="num__grid-item div1">1</button>
        <button @click="input(2)" class="num__grid-item div2">2</button>
        <button @click="input(3)" class="num__grid-item div3">3</button>
        <button @click="input('=')" class="num__grid-item div4">=</button>
        <button @click="input('.')" class="num__grid-item div5">.</button>
        <button @click="input(0)" class="num__grid-item div6">0</button>
      </div>
    </div>
  </div>
</template>

<script>
// import '@/assets/js/script.js'

export default {
  name: 'Calc',
  data() {
    return {
      result: ''
    }
  },
  methods: {
    input(char) {
      const panelBack = document.getElementById('panel__back')

      if (char === 'reset') {
        this.result = ''
        panelBack.innerHTML = '0'
        return
      }
      if (char === 'back') {
        this.result = this.result.substring(0, this.result.length - 1)
        console.log(this.result)
        return
      }
      if (char === '=') {
        panelBack.innerText = this.result
        this.result = eval(this.result).toString()
        return
      }
      this.result += char
    },

    changeTheme() {
      const themeButton = document.getElementById('theme-button')
      const darkTheme = 'dark-theme'
      const iconTheme = 'ri-sun-line'
      console.log(themeButton)

      const selectedTheme = localStorage.getItem('selected-theme')
      const selectedIcon = localStorage.getItem('selected-icon')

      const getCurrentTheme = () => document.body.classList.contains(darkTheme) ? 'dark' : 'light'
      const getCurrentIcon = () => themeButton.classList.contains(iconTheme) ? 'ri-moon-line' : 'ri-sun-line'

      if (selectedTheme) {
        document.body.classList[selectedTheme === 'dark' ? 'add' : 'remove'](darkTheme)
        themeButton.classList[selectedIcon === 'ri-moon-line' ? 'add' : 'remove'](iconTheme)
      }

      document.body.classList.toggle(darkTheme)
      themeButton.classList.toggle(iconTheme)
      localStorage.setItem('selected-theme', getCurrentTheme())
      localStorage.setItem('selected-icon', getCurrentIcon())
    }
  },
  watch: {
    result() {
      const input = document.getElementById('input')

      if (this.result.length <= 5) {
        input.style.fontSize = 7 + 'rem'
      }
      if (this.result.length > 5) {
        input.style.fontSize = 4 + 'rem'
      }
      if (this.result.length > 9) {
        input.style.fontSize = 2.5 + 'rem'
      }

    }
  },
}
</script>

<style scoped lang="scss">


</style>
