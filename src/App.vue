<template>
	<div class="app">
		<h1>Страница с постами</h1> 
		<my-input
			v-model="searchQuery"
			placeholder="Поиск"
		/>
		<div class="app__btns">
			<my-button
				@click="showDialog"
			> Создать пост</my-button>
			<my-select
				v-model="selectedSort"
				:options="sortOptions"
			></my-select>
		</div>
		<my-dialog v-model:show="dialogVisible">
			<PostForm
			@create="createPost"
		/>
		</my-dialog>
		
		<PostList  
			:posts="sortedAndSearchedPosts"
			@remove="removePost"
			v-if="!isPostsLoading"
		/>
		<div v-else> Идет загрузка...</div>
		<div class="page__wrapper">
			<div 
				v-for="pageNumber in totalPages" 
				:key="pageNumber" 
				class="page"
				:class="{
					'page_current': page === pageNumber
				}"
				@click="changePage(pageNumber)"
			> 
				{{ pageNumber }}
			</div>
		</div>
	</div>
</template>

<script>
import PostList from "@/components/PostList"
import PostForm from "@/components/PostForm"
import axios from "axios"
export default {
	components:{
		PostForm, PostList
	},
	data() {
		return{
			posts:[],
			dialogVisible: false,
			isPostsLoading:false,
			selectedSort:"",
			page: 1,
			limit:10,
			totalPages:0,
			sortOptions:[
				{value: "title", name:"По названию"},
				{value: "body", name:"По описанию"}
			],
			searchQuery:''
		}
	},
	methods:{
		createPost(post){
			this.posts.push(post);
			this.dialogVisible = false
		},
		removePost(post){
			this.posts = this.posts.filter(p => p.id != post.id)
		},
		showDialog(){
			this.dialogVisible = true
		},
		changePage(number){
			this.page = number,
			this.fetchPosts()
		},
		async fetchPosts() {
			try {
				this.isPostsLoading = true;
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts',{
					params:{
						_page: this.page,
						_limit:10
					}
				});
				this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
				this.posts = response.data;
			} catch (error) {
				alert (error)
			} finally {
				this.isPostsLoading = false;
			}
		}
	},
	mounted(){
		this.fetchPosts();
	},

	computed:{
		sortedPosts(){
			return [...this.posts].sort((post1,post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
		},
		sortedAndSearchedPosts(){
			return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
		}
	}
}
</script>

<style scoped>
*{
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

.app{
	padding: 20px;
}
.app__btns{
	display: flex;
	justify-content: space-between;
	margin-top:20px;
}
.page__wrapper{
	display: flex;
	gap: 10px;
	margin: 10px;
}
.page{
	display: flex;
	justify-content: center;
	align-items: center;
	border:  1px solid greenyellow;
	width: 25px;
	height: 25px;
	cursor: pointer;
}
.page_current{
	background-color: greenyellow;
	color: rgb(0, 54, 31);
}
</style>