<script lang="ts">
import 'giscus';

export default {
    props: {
        giscus: {
            repo: String,
            repoId: String,
            category: String,
            categoryid: String,
            term: String,
        }
    }
}
</script>

<template>
    <giscus-widget
            id="comments"
            :repo="giscus.repo"
            :repoid="giscus.repoId"
            :category="giscus.category"
            :categoryid="giscus.categoryid"
            mapping="specific"
            :term="giscus.term"
            reactionsenabled="1"
            emitmetadata="0"
            inputposition="top"
            theme="light"
            lang="en"
            loading="lazy"
    ></giscus-widget>
</template>

<style scoped>

</style>