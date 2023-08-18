<template>
    <button class="btn" >
        <slot></slot>
    </button>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
.btn{
	width: 100px;
	padding: 10px;
	background-color: greenyellow;
	color: black;
	border: 1px solid rgb(83, 138, 0);
}
</style>