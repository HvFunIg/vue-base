<template>
    <div>
        <h3>Список пользователей</h3>
    </div>
    <PostItem 
        v-for="post in posts"
        :post="post"
    >
    </PostItem>
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

</style>