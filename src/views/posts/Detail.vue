<script lang="js">

import axios from "axios";
import Giscus from "@/components/Giscus.vue";

export default {
    components: {Giscus},
    data() {
        return {
            post: null,
            postContent: null,
            giscus: null,
        };
    },
    created() {

    },
    mounted() {
        this.getPost(this.$route.params.id);
        this.getPostContent(this.$route.params.id);
    },
    methods: {
        async getPost(id) {
            const res = await axios.get('http://localhost:3000/app/posts/' + id);
            this.post = res.data;
            this.giscus = {
                repo: 'longlevan9x/notion-blog-comment',
                repoId: 'R_kgDOJe2r0g',
                category: 'Blog Comment',
                categoryid: 'DIC_kwDOJe2r0s4CWlBo'
            }
            this.giscus.term = this.post.title;
        },
        async getPostContent(id) {
            const res = await axios.get('http://localhost:3000/app/posts/' + id + '/content');
            this.postContent = res.data;
        },
        formatDate(dateString) {
            const date = new Date(dateString);
            // Then specify how you want your dates to be formatted
            return new Intl.DateTimeFormat('default', {dateStyle: 'long'}).format(date);
        }
    },
    watch: {}
}
</script>

<template>
  <!-- content
  ================================================== -->
    <section class="s-content">

        <div class="row">
            <div class="column large-12">

                <article class="s-content__entry format-standard" v-if="post">

                    <div class="s-content__media">
                        <div class="s-content__post-thumb">
                            <img :src="post.cover"

                                 sizes="(max-width: 2100px) 100vw, 2100px" alt="">
                            <!--                            srcset="images/thumbs/single/single-post-2100.jpg 2100w,-->
                            <!--                            images/thumbs/single/single-post-1050.jpg 1050w,-->
                            <!--                            images/thumbs/single/single-post-525.jpg 525w"-->
                        </div>
                    </div> <!-- end s-content__media -->

                    <div class="s-content__entry-header">
                        <h1 class="s-content__title s-content__title--post">{{ post.title }}</h1>
                    </div> <!-- end s-content__entry-header -->

                    <div class="s-content__primary">

                        <div class="s-content__entry-content" v-if="postContent" v-html="postContent"
                             style="width: 900px">
                        </div> <!-- end s-entry__entry-content -->

                        <div class="s-content__entry-meta">

                            <div class="entry-author meta-blk" v-for="author in post.authors">
                                <div class="author-avatar">
                                    <img class="avatar" src="images/doremon.png" alt="">
                                </div>
                                <div class="byline">
                                    <span class="bytext">Posted By</span>
                                    <RouterLink to="#0">{{ author.name }}</RouterLink>
                                </div>
                            </div>

                            <div class="meta-bottom">

                                <div class="entry-cat-links meta-blk">
                                    <div class="cat-links">
                                        <span style="margin-right: 5px">In</span>
                                        <RouterLink to="#0" v-for="tag in post.tags">{{ tag }}</RouterLink>
                                    </div>

                                    <span style="margin-right: 5px">On</span>
                                    {{ formatDate(post.published.start) }}
                                </div>

                                <div class="entry-tags meta-blk is-hidden">
                                    <span class="tagtext">Tags</span>
                                    <a href="#">orci</a>
                                    <a href="#">lectus</a>
                                    <a href="#">varius</a>
                                    <a href="#">turpis</a>
                                </div>

                            </div>

                        </div> <!-- s-content__entry-meta -->

                        <div class="s-content__pagenav">
                            <div class="prev-nav">
                                <a href="#" rel="prev">
                                    <span>Previous</span>
                                    Tips on Minimalist Design
                                </a>
                            </div>
                            <div class="next-nav">
                                <a href="#" rel="next">
                                    <span>Next</span>
                                    A Practical Guide to a Minimalist Lifestyle.
                                </a>
                            </div>
                        </div> <!-- end s-content__pagenav -->

                    </div> <!-- end s-content__primary -->
                </article> <!-- end entry -->

            </div> <!-- end column -->
        </div> <!-- end row -->

        <!-- comments
        ================================================== -->
        <div class="comments-wrap">

            <div id="comments" class="row">
                <div class="column large-12">
                    <Giscus :giscus="giscus" v-if="giscus"></Giscus>
                </div>
            </div>
        </div>

    </section> <!-- end s-content -->
</template>

<style scoped>

</style>