<template>
    <div class="message">
        <p>{{message}}</p>
    </div>
</template>

<script>
    export default {
        props: {
            message: {
                type: String,
                required: false,
                default: false
            }
        },
    };
</script>

<style lang="sass" scoped>
    .message
        text-align: center
        padding: 20px
</style>
