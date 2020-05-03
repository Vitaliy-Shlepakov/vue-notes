<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <h1>{{title}}</h1>

                    <message
                        v-if="errorMessage"
                        :message="errorMessage"
                    />

                    <!-- new note-->
                    <newNote
                        @addNote="addNewNote"
                        @throwNewMessage="throwNewMessage"
                    />

                    <!--note-list-->
                    <notes
                        :notesList="notes"
                        @removeNoteItem="removeNote"
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

    export default {
        components: {
            message,
            newNote,
            notes
        },

        data: function () {
            return {
                title: 'Notes',
                errorMessage: null,

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
            }
        }
    }
</script>

