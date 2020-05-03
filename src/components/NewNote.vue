<template>
    <div class="new-note">
        <label>Title</label>
        <input v-model="note.title" type="text">
        <label>Description</label>
        <textarea v-model="note.description"></textarea>
        <button class="btn btnPrimary add-btn" @click="addNote">New note</button>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                note: {
                    title: '',
                    description: ''
                },
            }
        },
        props: {

        },
        methods: {
            addNote: function () {
                const {title, description} = this.note;
                if (title.length == 0) {
                    this.$emit('throwNewMessage', 'Title can not be blank');
                    return;
                };
                this.$emit('addNote', this.note)
                this.clearNote()
                this.$emit('throwNewMessage', null);
            },
            clearNote: function () {
                this.note.title = '';
                this.note.description = '';
            }
        }
    }
</script>

<style lang="sass">

    .new-note
        text-align: center

    .add-btn
        margin: 20px 0 0
        display: inline-block
        transition: background-color .2s

        &:hover
            background-color: darken(#494ce8, 10%)!important
</style>