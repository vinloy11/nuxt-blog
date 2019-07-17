<template>
    <div class="container">
        <h2 class="mb-3">{{user.name}} Profile</h2>
        <h2 class="mb-3">User email: {{user.email}} </h2>
    </div>
</template>

<script>
    export default {
        middleware: ['auth'],

    }
</script>

<style scoped>

</style>
