<template>
    <div>
        <form @submit="addBook">
            <input type="text" name="title" v-model="title" placeholder="Add Book">
                <input type="submit" value="Submit" class="btn btn-info">
        </form>
    </div>
</template>

<script>
    export default {
        name: "AddBookItem",
        props: ['editBook'],
        data () {
            return {
                title: '',
                id: '',
                edit: false
            }
        },
        methods: {
            addBook(e){
                e.preventDefault();
                if (this.edit === false){
                    // add new book
                    const newBook = {
                        title: this.title,
                        id: Math.floor(Math.random() * 100)
                    };
                    if (newBook.title !== ''){
                        this.$emit('add-book-event', newBook);
                    }
                    this.title = ''
                }else{
                    //edit book
                    const bookItem = {
                        title: this.title,
                        id: this.id
                    };
                    //send to parent (App.vue)
                    this.$emit('edit-book-event', bookItem);
                    // clear input field
                    this.title = '';
                    this.edit = false;
                }
            }
        },
        watch: {
            editBook: {
                handler() {
                    this.title = this.editBook.title;
                    this.id = this.editBook.id;
                    this.edit = true
                },
                deep: true
            },
            title:{
                handler(){
                    if(this.title === ''){
                        this.edit = false;
                    }
                }
            }
        }
    }
</script>

<style scoped>

</style>
