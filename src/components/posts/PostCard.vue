<script lang="js">
export default {
    props: {
        post: {
            id: '',
            cover: '',
            title: '',
            authors: [],
            description: ''
        }
    }
}
</script>

<template>
    <div class="entry__thumb">
        <RouterLink :to="post.id" class="thumb-link">
            <img :src="post.cover ?? '/images/eye.png'"
                 alt="">
            <!--   :srcset="post.cover +' 1x,' + post.cover +' 2x,'"-->

        </RouterLink>
    </div> <!-- end entry__thumb -->

    <div class="entry__text">
        <div class="entry__header">
            <h1 class="entry__title">
                <RouterLink :to="post.id">{{ post.title }}</RouterLink>
            </h1>

            <div class="entry__meta">
                                        <span class="byline">By:
                                            <span class='author' v-for="author in post.authors">
                                                <a href="#">{{ author.name }}</a>
                                            </span>
                                        </span>

            </div>
        </div>
        <div class="entry__excerpt">
            <p>
                {{ post.description }}
            </p>
        </div>
        <RouterLink :to="post.id" class="entry__more-link">Learn More</RouterLink>
    </div> <!-- end entry__text -->
</template>

<style scoped>

</style>