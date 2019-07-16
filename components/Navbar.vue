<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light fixed-top">
        <nuxt-link to="/" class="navbar-brand">Frontend</nuxt-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <nuxt-link active-class="active" to="/" class="nav-link" exact>Home</nuxt-link>
                </li>
                <li class="nav-item">
                    <nuxt-link active-class="active" to="/topics" class="nav-link" exact>Topics</nuxt-link>
                </li>
                <li class="nav-item">
                    <nuxt-link active-class="active" to="/posts" class="nav-link">Posts</nuxt-link>
                </li>
                <li class="nav-item">
                    <nuxt-link active-class="active" to="/dashboard" class="nav-link">Create</nuxt-link>
                </li>
            </ul>
            <template v-if="!authenticated">
                <ul class="navbar-nav ml-auto">
                    <li class="nav-item ">
                        <nuxt-link active-class="active" to="/login" class="nav-link">Login</nuxt-link>
                    </li>
                    <li class="nav-item">
                        <nuxt-link active-class="active" to="/register" class="nav-link">Register</nuxt-link>
                    </li>
                </ul>
            </template>
            <template v-else>
                <ul class="navbar-nav ml-auto">
                    <li class="nav-item">
                        <nuxt-link active-class="active" to="/profile" class="nav-link" exact>{{user.name}}</nuxt-link>
                    </li>
                    <li class="nav-item">
                        <a style="cursor: pointer" @click.prevent="logout" class="nav-link">Logout</a>
                    </li>
                </ul>
            </template>
        </div>
    </nav>
</template>

<script>
    export default {
        methods: {
            logout() {
                this.$auth.logout()
            }
        }
    }
</script>

<style scoped>

</style>
