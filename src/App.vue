<template>
  <div id="app" class="container">
    <div class="pageHeader">
        <h1>Bookmarks App</h1>
    </div>
    <div class="panel panel-default">
        <div class="panel-heading">
            <h3>Add new bookmark</h3>
        </div>
        <div class="panel-body">
            <form id="form" class="form-inline">
                <div class="form-group">
                    <label for="bookTitle">Title:</label>
                    <input v-model="newBook.title" type="text" class="form-control" id="bookTitle">
                </div>
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
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="book in books">
                        <td><a v-bind:href="book.url">{{book.title}}</a></td>
                        <td>{{book.author}}</td>
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
