<template>
  <div id="app" class="container">
    <div class="pageHeader">
        <h1>Bookmarks App</h1>
    </div>
    <div>
        <div>
            <h3>Add new bookmark</h3>
        </div>
        <div>
            <form id="form" class="form-inline" v-on:submit.prevent = "addBookmark">
                <div class="form-group">
                    <label for="bookTitle">Title:</label>
                    <input v-model="newBook.title" type="text" class="form-control" id="bookTitle">
                </div>
                <div class="form-group">
                    <label for="bookAuthor">Author:</label>
                    <input v-model="newBook.author" type="text" class="form-control" id="bookAuthor">
                </div>
                <div class="form-group">
                    <label for="bookUrl">Url:</label>
                    <input v-model="newBook.url" type="text" class="form-control" id="bookUrl">
                </div>
                <input type="submit" class="btn btn-primary" value="Add bookmark">
            </form>
        </div>
    </div>
    <div class="panel panel-default">
        <div class="panel-heading">
            <h3>Books list</h3>
        </div>
        <div class="panel-body">
            <table class="table table-striped">
                <thead>
                    <tr>
                        <th>Title</th>
                        <th>Author</th>
                        <th>Remove</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="book in books">
                        <td><a v-bind:href="book.url">{{book.title}}</a></td>
                        <td>{{book.author}}</td>
                        <td><span class="glyphicon glyphicon-remove" v-on:click="remove(book)"><i class="fa fa-trash-o" aria-hidden="true"></i></span></td>
                    </tr>
                    
                </tbody>
            </table>
        </div>
    </div>
  </div>
</template>

<script>
    import Firebase from 'firebase' // 1 importing the firebase

    // 2 create a config wich one can be downloaded from my firebase
    let config = {
        apiKey: "AIzaSyAZK1YBXMuYOspMrl8HsXUjSBzeXnJo6eM",
        authDomain: "vuejs-firebase-app-114ef.firebaseapp.com",
        databaseURL: "https://vuejs-firebase-app-114ef.firebaseio.com",
        projectId: "vuejs-firebase-app-114ef",
        storageBucket: "vuejs-firebase-app-114ef.appspot.com",
        messagingSenderId: "12696200737"
    }

    // 3 initialize app
    let app = Firebase.initializeApp(config)
    // 4 adding conection to database
    let db = app.database();
    // 5 choose what we want from database which is books object (reference)
    let booksRef = db.ref('books')


    export default {
        name: 'app',
        // add the property firebase
        firebase: {
            books: booksRef // adding our books easly. so we have access to object form database
        },
        data(){
            return{
                newBook:{
                    title:"",
                    author:"",
                    url:""
                }
            }
        },
        methods:{
            addBookmark:function(){
                booksRef.push(this.newBook);
                this.newBook.title = "";
                this.newBook.author = "";
                this.newBook.url = "";
            },
            remove:function(book){
                booksRef.child(book['.key']).remove()
            }
        }
    }

</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
        margin-top: 60px;
    }

</style>
