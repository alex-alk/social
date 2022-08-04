<template>
    <div class="flex flex-col py-4 max-w-xl mx-auto">
        <NewPost />
        <Post
            v-if="posts"
            v-for="post in posts"
            :key="post.post_id"
            :post="post"
            @scroll="handleScroll($e)"
        />
        <LoadMore :posts="posts" />
    </div>
</template>

<script>
import NewPost from "../components/NewPost";
import Post from "../components/Post";
import { mapGetters } from "vuex";
import LoadMore from "../components/LoadMore";

export default {
    name: "NewsFeed",

    components: {
        NewPost,
        Post,
        LoadMore,
    },
    mounted() {
        this.$store.dispatch("fetchAllPosts");
    },
    computed: {
        ...mapGetters(["posts", "loadmorestatus"]),
    },
    methods: {
        handleScroll(e) {
            var currentScrollPosition = e.srcElement.scrollTop;
            if (currentScrollPosition > this.scrollPosition) {
                console.log("Scrolling down");
            }
            this.scrollPosition = currentScrollPosition;
            console.log("down");
            this.$store.dispatch("loadmore", posts.meta);
        },
    },
};
</script>

<style scoped></style>
