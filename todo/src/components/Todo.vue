<template>
    <button class="list-group-item text-left" @click="clickButton">
        {{ label }}
    </button>
</template>
<script>
    export default {
        props:['label'],// 외부에서 입력받을 label을 props에 지정
        methods: {
            clickButton(){
                this.$emit('componentClick'); 
            }
        }
    };
</script>