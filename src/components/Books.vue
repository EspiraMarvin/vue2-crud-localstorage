<template>
    <div>
        <h2>My Books List</h2>
        <div v-bind:key="book.id" v-for="book in books">
            <BookItem v-bind:book="book" v-on:del-book-item="delBookMethod" v-on:edit-book-item="editBookMethod" />
        </div>
        <div v-if="!books.length">
            <p>No Books to Read!!</p>
        </div>
    </div>
</template>

<script>
    import BookItem from "./BookItem";
    export default {
        name: "Books",
        props: ["books"],
        components: {
            BookItem
        },
        methods: {
            delBookMethod(id){
                //send to parent
                this.$emit('del-book-event', id);
            },
            editBookMethod(id){
                //send to parent (App.vue)
                this.$emit('edit-book-event', id)
            }
        }
    }
</script>

<style scoped>

</style>
