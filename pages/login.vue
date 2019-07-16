<template>
    <div class="container col-md-6 pt-5">
        <h2 class="mb-3">Login</h2>
        <hr>
        <form @submit.prevent="submit">
            <div class="form-group">
                <label>Email address</label>
                <input
                        v-model.trim="form.email"
                        type="email"
                        class="form-control"
                        placeholder="Enter email"
                        autofocus
                >
                <small class="form-text text-danger" v-if="errors.email">{{ errors.email[0] }}</small>
            </div>
            <div class="form-group">
                <label>Password</label>
                <input
                        v-model.trim="form.password"
                        type="password"
                        class="form-control"
                        placeholder="Password">
                <small class="form-text text-danger" v-if="errors.password">{{ errors.password[0] }}</small>
            </div>
            <button type="submit" class="btn btn-primary">Login</button>
        </form>
        <p class="mt-3">Don't have an account? <nuxt-link class="stretched-link" to="/register">Register</nuxt-link></p>
    </div>
</template>

<script>
    export default {
        middleware: ['guest'],
        data() {
            return {
                form: {
                    email: '',
                    password: ''
                }
            }
        },
        methods: {
            async submit() {
                await this.$auth.loginWith("local", {
                    data: this.form
                })

                this.$router.push({
                    path: this.$route.query.redirect || '/profile'
                })
            }
        }
    }
</script>

<style scoped>

</style>
