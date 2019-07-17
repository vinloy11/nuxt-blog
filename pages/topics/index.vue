<template>
    <div class="container">
        <h1>Latest topics</h1>
        <div v-for="(topic, index) in topics" :key="index" class="bg-light mt-5 mb-5" style="padding: 20px">
            <h2>{{ topic.title }}</h2>
            <p class="text-muted" style="font-size: 12px">{{ topic.created_at }} by {{ topic.user.name }}</p>

            <div v-for="(content, index) in topic.posts" :key="index" class="ml-5 content">
                {{ content.body }}
                <p class="text-muted" style="font-size: 10px">{{ content.created_at }} by {{ content.user.name }}</p>
            </div>
        </div>

        <nav>
            <ul class="pagination justify-content-center">
                <li v-for="(key, value) in links" class="page-item">
                    <a @click="loadMore(key)" href="#" class="page-link">{{value}}</a>
                </li>
            </ul>
        </nav>

    </div>
</template>

<script>
    export default {
        middleware: ['auth'],
        data() {
            return {
                topics: [],
                links: []
            }
        },
        async asyncData({$axios}) {
            let {data, links} = await $axios.$get('/topics')
            // console.log(links)
            return {
                topics: data,
                links
            }
        },

        methods: {
            async loadMore(key) {
                let {data} = await this.$axios.$get(key)
                return this.topics = {...this.topics, ...data}
            }
        }
    }
</script>

<style lang="scss" scoped>
    .content {
        border-left: 10px solid white;
        padding: 0 10px 0 10px;
    }
</style>
