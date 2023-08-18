<template>
    <input type="text" :value="modelValue" @input="updateInput">
</template>

<script>
    export default {
        name:'my-input',
        props:{
            modelValue: [String,Number]
        },
        methods: {
            updateInput(event){
                this.$emit('update:modelValue', event.target.value)
            }
        }
    }
</script>

<style scoped>
input{
	border: 1px solid greenyellow;
	padding: 10px 15px;
	margin-top: 10px;
}
</style>