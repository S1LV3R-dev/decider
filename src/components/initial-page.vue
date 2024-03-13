<template>
    <div class="mb-3">
    <h1>
        Ask a question
    </h1>
      <input v-model="question" name="question" type="text" class="form-control" id="question">
      <button class="btn animate__animated animate__fadeIn" v-if="question" @click="handleNext">
        Next
      </button>
    </div>
</template>

<script>
export default{
    data(){
        return {
            question:'',
            error:false
        }
    },
    methods:{
        handleNext(e){  
            e.preventDefault();
            if(this.question.length < 5){
                this.$emit('toast',{message:"Question is too short", type:'error'});
            } else if(this.question.length >= 50) {
                this.$emit('toast',{message:"Question is too long", type:'error'});
            } else {
                this.error=false;
                this.$emit('goto', 1);
                this.$emit('question', this.question);
            }
        }
    }
}
</script>