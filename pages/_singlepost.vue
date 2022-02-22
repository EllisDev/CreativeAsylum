<template>
    <div class="div">
        Slug: {{ this.post.slug }} <br />
        Title: {{ this.post.title }} <br />
        <div v-html="this.post.content" class="div"></div>

        <a href="/blog">Go back to homepage</a>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Post',

    data() {
        return {
            post: [],
            error: '',
            postid: 'this-is-the-third-post',
        }
    },

    created() {
        axios
            .request({
                method: 'get',
                baseURL:
                    process.env.BLOG_API_URL1 +
                    process.env.BUCKET_NAME +
                    '/object' +
                    $nuxt.$route.path +
                    '?pretty=true&props=title,content,slug&read_key=' +
                    process.env.READ_ID,
            })
            .then((response) => {
                this.post = response.data.object
            })
            .catch((error) => {
                this.error = error
            })
    },
}
</script>
