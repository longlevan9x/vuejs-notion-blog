<script lang="ts">
import PostCard from "@/components/posts/PostCard.vue";

export default {
    components: {PostCard},
    props: {
        posts: []
    }
}
</script>

<template>
    <div v-masonry transition-duration="0.3s" item-selector=".item">
        <article v-masonry-tile class="item masonry__brick entry format-standard brick entry"
                 data-aos="fade-up"
                 v-for="post in posts">

            <PostCard :post="post"></PostCard>

        </article> <!-- end article -->

    </div> <!-- end brick-wrapper -->
</template>

<style scoped>

</style>