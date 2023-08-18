<template>
    <form @submit.prevent>
			<h4> Создание поста</h4>
			<input 
                v-model="post.title"
				type="text"
				placeholder="Назвавние"
            >
            <input 
                v-model="post.body"
				type="text" 
				placeholder="Описание"
            >
			<!-- <button class="btn" @click="createPost"> Создать</button> -->
		</form>
</template>

<script>
    export default {
        data(){
            return{
                post:{
                    title:'',
                    body:''
                }
            }
        }
    }
</script>

<style scoped>
.btn{
	width: 100px;
	align-self: flex-end;
	margin-top: 15px;
	padding: 10px;
	background-color: greenyellow;
	color: black;
	border: 1px solid rgb(83, 138, 0);
}

input{
	width: 100%;
	border: 1px solid greenyellow;
	padding: 10px 15px;
	margin-top: 10px;
}
form{
	display: flex;
	flex-direction: column;
}
</style>