<template>
    <div class="container">
        <a @click="goBack" class="link text-success">Back</a>
        <div class="bg-light mt-5 mb-5" style="padding: 20px">
            <h2 class="display-3">{{ topic.title }}</h2>
            <hr>

            <p class="text-muted" style="font-size: 12px">{{ topic.created_at }} by {{ topic.user.name }}</p>

            <div v-for="(content, index) in topic.posts" :key="index" class="ml-5 content">
                {{ content.body }}
                <p class="text-muted" style="font-size: 10px">{{ content.created_at }} by {{ content.user.name }}</p>
            </div>
        </div>
        <div class="mt-5 ml-5 mr-5 mb-5" v-if="authenticated">
            <form @submit.prevent="create($route.params.id)">
                <div class="form-group">
                    <h4>Add a new post:</h4>
                    <textarea
                            v-model="body"
                            class="form-control"
                            rows="5"
                            placeholder="Write something..."
                    ></textarea>
                    <!---->
                    <small v-if="errors.body" class="form-text text-danger">
                        {{ errors.body[0] }}
                    </small>
                </div>
                <button class="btn btn-outline-primary">
                    Add a new post
                </button>
            </form>
        </div>
        <!--<nuxt-link @click="goBack" to="" class="link text-success">Back</nuxt-link>-->
        <a @click="goBack" class="link text-success">Back</a>
        <!--<nuxt-link to="/posts">prev</nuxt-link>-->
    </div>
</template>

<script>
    export default {
        data() {
            return {
                topic: '',
                body: '',
                // value: '',
            }
        },
        async asyncData({$axios, params}) {
            const {data} = await $axios.$get(`/topics/${params.id}`)
            return {
                topic: data
            }
        },
        methods: {
            async create(id) {
                await this.$axios.$post(`/topics/${this.$route.params.id}/posts`, {
                    body: this.body
                })
                let {data} = await this.$axios.$get(`/topics/${id}`)
                this.body = ''
                return this.topic = {...this.topic, ...data}
            },
            goBack() {
                return this.$router.go(-1)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .link, a {
        color: deepskyblue;
        font-size: 16px;
        cursor: pointer;
        font-weight: bold;
    }
</style>
