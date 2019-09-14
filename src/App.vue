<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1 class="text-center">Super Quiz!</h1>
      </div>
    </div>
    <hr>
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <transition name="flip" mode="out-in">
          <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-questions'"></component>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Answer from './components/Answer.vue'
import Questions from './components/Questions.vue'

export default {
  name: 'app',
  data(){
    return {
      mode: 'app-answer'
    }
  },
  methods: {
    answered(isCorrect){
     if(isCorrect){
       this.mode = 'app-answer'
     }else{
       this.mode = 'app-questions'
       alert('try again')
     }
    }
  },
  components: {
    appAnswer: Answer,
    appQuestions: Questions
  }
}
</script>

<style>

.flip-enter{
  /*transform: rotateY(0deg);*/
}
.flip-enter-active{
  animation: flip-in 0.15s ease-out forwards;
}
.flip-leave{
  /*transform: rotateY(0deg);*/
}
.flip-leave-active{
  animation: flip-out 0.15s ease-out forwards;
}

@keyframes flip-out {
  from{
    transform: rotateX(0deg)
  }
  to{
    transform: rotateX(90deg)
  }
}
@keyframes flip-in {
  from{
    transform: rotateY(90deg)
  }
  to{
    transform: rotateY(0deg)
  }
}
</style>
