<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <!-- message-->
                    <message
                        v-if="errorMessage"
                        :message="errorMessage"
                    />

                    <!-- new note-->
                    <newNote
                        @addNote="addNewNote"
                        @throwNewMessage="throwNewMessage"
                    />

                    <!-- notes header-->
                    <div class="note-header">
                        <h1>{{title}}</h1>

                        <div class="icons-controls">
                            <!--search-->
                            <p>{{search}}</p>
                            <search
                                :value="search"
                                placeholder="Find your note"
                                @searchNote="val => search = val"
                            />
                        </div>

                        <div class="note-icons">
                            <span
                                    class="note-icon"
                                    :class="{active: grid}"
                                    @click="grid = true"
                            >
                                <iconRow/>
                            </span>
                            <span
                                    class="note-icon"
                                    :class="{active: !grid}"
                                    @click="grid = false"
                            >
                                <iconList/>
                            </span>
                        </div>
                    </div>

                    <!--note-list-->
                    <notes
                        :notesList="notesFilter(notes)"
                        @removeNoteItem="removeNote"
                        :grid="grid"
                    />
                </div>
            </section>
        </div>
    </div>
</template>

<script>
    import message from './components/Message.vue';
    import newNote from './components/NewNote.vue';
    import notes from './components/Notes.vue';
    import search from './components/Search.vue';
    import iconList from './components/IconList.vue';
    import iconRow from './components/IconRow.vue';

    export default {
        components: {
            message,
            newNote,
            notes,
            iconList,
            iconRow,
            search
        },

        data: function () {
            return {
                title: 'Notes App',
                errorMessage: null,
                grid: true,
                search: '',
                notes: [
                    {
                        title: 'First note',
                        description: 'Description for first note',
                        date: new Date(Date.now()).toLocaleString()
                    },
                    {
                        title: 'Second note',
                        description: 'Description for second note',
                        date: new Date(Date.now() + 1000).toLocaleString()
                    },
                    {
                        title: 'Third note',
                        description: 'Description for third note',
                        date: new Date(Date.now() + 2000).toLocaleString()
                    },
                ]
            }
        },

        methods: {
            addNewNote: function(newNote){
                this.notes.push({
                    ...newNote,
                    date: new Date(Date.now()).toLocaleString()
                });
            },
            throwNewMessage: function(message){
                this.errorMessage = message;
            },
            removeNote: function(index){
                this.notes.splice(index, 1)
            },
            notesFilter(notes){
                if(!this.search){
                    return notes;
                };
                notes = notes.filter((note) => {
                    if(note.title.toLowerCase().indexOf(this.search.toLowerCase()) !== -1){
                        return note
                    }
                });
                return notes
            }
        },
    }
</script>

<style lang="sass">

    .note-header
        display: flex
        justify-content: space-between

    .note-icon
        display: inline-block
        width: 24px
        height: 24px

        svg
            max-width: 100%
            height: 100%
            fill: #ccc
            stroke: #ccc
            transition: all .2s

        &:first-child
            margin-right: 10px

        &:hover
            cursor: pointer

            svg
                fill: #222
                stroke: #222

        &.active
            svg
                fill: #222
                stroke: #222

</style>

