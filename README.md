# Базовые знания о Vue 3

### 1. Директива *v-on* также записывается как @
```
<button v-on:click="addLike"> Like </button>
<button @click="addDislike"> Dislike </button>
```
### 2. Директива *v-bind* также записывается как :
```
<button v-bind:props="props"> Like </button>
<button :props="props"> Like </button>
```
### 3. Изолирование стилей в компоненте:
```
<style scoped>
...
</style>
```
### 4. Двустороннее связывание через v-bind
```
    <input v-bind:value="title" type="text" placeholder="Назвавние">
    <input v-bind:value="body" type="text" placeholder="Описание">

      data() {
        return{
           title:'',
           body:''
        }
    },
```
### 5. Модификаторы
Во Vue есть модификаторы, которые упрощают работу с событиями. Например, навесить *preventDefault* можно так :
```
<form @submit.prevent>
```
### 6. Импорт компонента
#### Локальный импорт:
```
<script>
import PostList from "@/components/PostList"
import PostForm from "@/components/PostForm"
export default {
	components:{
		PostForm, PostList
	},
    ...
}
```
#### Глобальный импорт
```
import components from '@/components/UI'

const app = createApp(App)

components.forEach(component =>{
    app.component(component.name, component)
})
app.mount('#app')

```
### 7. Двустороннее связывание также может быть осуществлено через *v-model*, тогда не нужно прописывать *v-bind*

### 8. Данные от ребенка к родителю передаются через $emit

**Дочерний компонент:**
```
createPost(){
    this.$emit('create',this.post)
    this.post = {
        title: "",
        body: ""
    }
}
```
**Родительский компонент:**
```
<PostForm
    @create="createPost"
/>
```

### 9. Жизненный цикл
Используются методы, аналогичные хукам в реакте. Например *mounted(){}*
### 10. Наблюдаемые и вычисляемые свойства 
*watch* - аналог *useEffect()*
*computed* - *useMemo()*
```
<template>
    <PostList  
			:posts="randomName"
		/>
</template>

...

data() {
		return{
			selectedSort:"",
		}
	},
	watch:{
		selectedSort(newValue){

        }
	},
    computed:{
        randomName(){}
    }
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
