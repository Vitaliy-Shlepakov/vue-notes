<template>
    <div class="notes">
        <div
                class="note"
                v-for="(note, index) in notesList"
        >
            <div class="note-header">
                <p>{{ note.title }}</p>
                <p class="note-delete" @click="()=> removeNote(index)">&times;</p>
            </div>
            <div class="note-body">
                <p>{{ note.description }}</p>
                <span>{{ note.date }}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            notesList: {
                type: Array,
                required: false,
                default: []
            }
        },
        methods: {
            removeNote(index) {
                this.$emit('removeNoteItem', index)
            }
        }
    };
</script>

<style lang="sass">
    .notes
        display: flex
        align-items: center
        justify-content: space-between
        flex-wrap: wrap
        padding: 40px 0

    .note
        width: 46%
        padding: 18px 20px
        margin-bottom: 20px
        background-color: #fff
        position: relative

    .note-body
        p
            margin: 20px 0

        span
            font-size: 14px
            color: #999

    .note-header
        p
            color: #402bad
    
    .note-delete
        font-size: 26px
        position: absolute
        right: 20px
        top: 20px

        &:hover
            cursor: pointer

</style>
