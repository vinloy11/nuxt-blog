<template>
    <div class="container">
        <h1>Latest topics</h1>
        <div v-for="(topic, index) in topics" :key="index" class="bg-light mt-5 mb-5" style="padding: 20px">
            <h2><nuxt-link style="text-decoration: none;" class="link" :to="{name: 'topics-id', params: {id: topic.id} }" >{{ topic.title }}</nuxt-link></h2>

            <div v-if="authenticated">
                <div v-if="user.id === topic.user.id">
                    <nuxt-link :to="{name: 'topics-edit', params: {id: topic.id} }">
                        <button class="btn btn-outline-success fa fa-edit fa-2x float-right">
                        </button>
                    </nuxt-link>
                    <button
                            @click="deleteTopic(topic.id)"
                            class="btn btn-outline-danger fa fa-trash fa-2x float-right">
                    </button>
                </div>
            </div>

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
            },
            async deleteTopic(id) {
                await this.$axios.$delete(`/topics/${id}`)
                let {data} = await this.$axios.$get(`/topics`)
                return this.topics = {...this.topics, ...data}
                // this.$router.push('/')
            }
        }
    }
</script>

<style lang="scss" scoped>
    .content {
        border-left: 10px solid white;
        padding: 0 10px 0 10px;
    }
    .link {
        color: black;
        &:hover {
            color: slategray;
        }
    }
    .btn-outline-success, .btn-outline-danger {
        border: none;
    }
</style>
