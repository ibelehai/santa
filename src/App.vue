<template>
  <div id="app">
    <div class="block" v-if="currentStep === 0 && !success">
      <h1>Хвилинка тролінгу</h1>
      <p style="font-size: 1.5rem">{{ topText }}</p>
      <h1 v-if="nayobCount !== 2" style="font-size: 4rem">{{ showText ? text : countDown }}</h1>
      <img style="width: 320px" v-if="nayobCount < 2 && !showText" src="https://media.giphy.com/media/cklPOHnHepdwBLRnQp/giphy.gif" />
      <span style="display: block; margin-bottom: 1rem" v-if="nayobCount === 1 && showText">Для особо одаренных - одна кнопка)</span>
      <div v-if="showInput">
        <input type="password" style="padding: 1rem 2rem; font-size: 1rem" v-model="code" />
      </div>
      <div style="margin-top: 1rem" v-if="showText || nayobCount === 2">
        <button class="btn" style="margin-right: 0.5rem" v-if="nayobCount === 0" @click="daliClick">Далі</button>
        <button class="btn" @click="daliClick">Далі</button>
      </div>
    </div>
    <div v-if="success" class="block">
      <h1>Вітаю)</h1>
      <p v-if="envy">Досі не знаєш, що відбувається? Ок. тримай...</p>
      <img style="width: 320px" src="https://media.giphy.com/media/9YlhdI9SSP0Qw/giphy.gif" />
    </div>
  </div>
</template>



<script>
  export default {
    name: 'App',
    data() {
      return {
        countDown : 0,
        currentStep: 0,
        showText: false,
        showInput: false,
        answer: null,
        topText: '',
        success: false,
        text: '',
        code: '',
        envy: false,
        nayobCount: 0,
      }
    },
    methods: {
      countDownTimer() {
        if(this.countDown !== 45) {
          setTimeout(() => {
            this.showText = false;
            this.countDown += 1
            this.countDownTimer()
          }, 1000)
        } else {
          this.showText = true;
          this.text = 'Ок. Тисни "Далі"'
        }
      },
      daliClick() {
        this.countDown = 0;

        if (this.nayobCount === 0) {
          this.showText = false;
          this.topText = 'Ти вибрав погану кнопку. Чекай ще раз)';
          this.countDownTimer();
        } else if (this.nayobCount === 1) {
          this.topText = 'Маю переконатись, що це ти. Введи код, який знаходиться під кавовою машинкою'
          this.countDown = null;
          this.showInput = true;
        } else if (this.nayobCount === 2) {
          if (this.code === 'zth1VtW138b00bRGCTsSk') {
            this.success = true;
            window.scrollTo(0, 0);
            setTimeout(() => {
              this.envy = true;
            }, 5000)
            setTimeout(() => {
              window.location.href = '/certificate.pdf'
            }, 8000)
          } else {
            window.alert('Уви, давай з початку. Не можу бути впевненим, що це справді ти')
            window.location.reload();
          }
        }

        this.nayobCount += 1;
      },

      generateButton() {

      }
    },
    created() {
      this.topText = 'Просто так нічого не дається, треба почекати...'
      this.countDownTimer()
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
    font-size: 1rem;
  }

  .block {
    text-align: center;
  }

  .btn {
    background-color: cornflowerblue;
    color: white;
    padding: 1rem 2rem;
    border-radius: 8px;
    font-size: 1rem;
    border: none;
    outline: none;
  }

</style>
