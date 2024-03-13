<template>
    <div>
        <h3>
            Your answer is:
        </h3>
        <div class="viewer">
            {{ result }}
        </div>
        <div class="animate__animated">
            <button class="btn" @click="startOver">Start over</button>
            <button class="btn" @click="newResult">Decide again</button>
        </div>
    </div>
</template>

<script>

export default{
    props:['result'],
    mounted(){
        this.$emit('genResult');
    },
    methods:{
        startOver(){
            this.$emit('startOver');
        },
        newResult(){
            this.$emit('genResult');
        }
    }
}

</script>