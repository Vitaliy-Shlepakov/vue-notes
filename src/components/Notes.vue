<template>
    <div class="notes" :class="">
        <div
                :class="[{'note-full': !grid}, 'note']"
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
            },
            grid: {
                type: Boolean
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
        border-radius: 3px
        box-shadow: 2px 2px 10px rgba(0,0,0, .1)
        transform: translateY(0)
        transition: transform .3s, width .2s

        &.note-full
            width: 100%

        &:hover
            transform: translateY(-5px)

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
        transform: scale(1)
        transition: transform .2s

        &:hover
            cursor: pointer
            transform: scale(1.2)
</style>
