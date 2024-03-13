<template>
  <div class="container">
    <Transition name="fade" appear mode="out-in">
      <component :result="result" :question="question" @toast="handleToast" @startOver="startOver"
        @genResult="decideResult" @question="saveQuestion" @goto="changePage" :is="screens[position]"></component>
    </Transition>
  </div>
</template>

<script>
import appInitial from './components/initial-page.vue'
import appConfirm from './components/confirm-page.vue'
import appResults from './components/results-page.vue'
export default {
  components: {
    appInitial,
    appConfirm,
    appResults
  },
  data() {
    return {
      list: ['Yes', 'No', 'Maybe', 'Not sure... Try again', 'Ask a friend'],
      screens: ["appInitial", "appConfirm", "appResults"],
      position: 0,
      question: '',
      result: '',
    }
  },
  methods: {
    handleToast(values) {
      console.log(1)
      this.$toast.show(values.message, { type: values.type, position: 'top', duration: 2000, pauseOnHover: false });
    },
    changePage(position) {
      this.position = position;
    },
    saveQuestion(question) {
      this.question = question;
    },
    generateResult() {
      return this.list[Math.floor(Math.random() * this.list.length)]
    },
    decideResult() {
      let rand = this.generateResult();
      if (rand !== '') {
        while (rand === this.result) {
          rand = this.generateResult();
        }
      }
      this.result = rand;
    },
    startOver() {
      this.position = 0;
      this.question = '';
      this.result = '';
    }
  }
}

</script>

<style>
@import url('./assets/style.css');

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: .5s;
}

.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: .5s;
}

.fade-leave-to {
  opacity: 0;
}
</style>
