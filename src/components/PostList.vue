<template>
    <div v-if="posts.length >0">
        <h3>Список поcтов</h3>
        <transition-group name="user-list">
            <PostItem 
                v-for="post in posts"
                :post="post"
                :key="post.id"
                @remove="$emit('remove',post)"
                >
            </PostItem>
        </transition-group>
    </div>
    <h2 v-else style="color:red"> Список пользователей пуст</h2>
</template>

<script>
import PostItem from './PostItem.vue';

    export default {
    props: {
        posts: {
            type: Array,
            required: true
        }
    },
    components: { PostItem }
}
</script>

<style scoped>
.user-list{
    display: inline-block;
    margin-right: 10px;
}
.user-list-enter-active, .user-list-leave-active{
    transition: all .3s ease
}
.user-list-enter-from, .user-list-leave-to{
    opacity:0;
    transform: translateY(30px)
}
.user-list-move{
    transition: transform .4s ease
}
</style>