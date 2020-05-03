<template>
    <div class="wrapper__search">

        <div class="search">
            <div class="search-icon">

            </div>
            <input
                type="text"
                :placeholder="placeholder"
                v-model.trim="search"
            >
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
            required: true
        },
        placeholder: {
            type: String,
            default: 'Search'
        },
    },
    data() {
        return {
            search: this.value
        }
    },
    watch: {
        search(val) {
            this.$emit('searchNote', val);
        }
    }
}
</script>

<style lang="sass" scoped>

</style>