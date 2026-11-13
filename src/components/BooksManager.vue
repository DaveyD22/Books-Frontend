<script setup>
import { createBook, deleteBook, getBooks } from '../api/books';


</script>
<script>
    export default{
        name: "BooksManager",
        data(){
            return{
                books: [],
                newBook:{
                    title: "",
                    author: "",
                    year: 2000,

                }
            };
        },
        methods:{
            async loadbooks(){
                this.books = await getBooks();
            },
            async addBooks(book){
                await createBook(book);
                await this.loadbooks();
            },
            async submitCreateBook(){
                await this.addBooks(this.newBook);
            },
            async removeBook(id){
                await deleteBook(id);
                await this.loadbooks();
            }
        },
        mounted(){
            this.loadbooks();
        }
    };
</script>
<template>
    <main class="">
        <h1>Konyvtar Kezelo</h1>


        <form @submit.prevent="submitCreateBook" class="w-full m-10 my-10 border-2 border-stone-200 p-3 flex flex-col">
            <div><label for="title">Cim:</label>
            <input v-model="newBook.title" type="text" name="title" /></div>

            <div><label for="author">Szerzo:</label>
            <input v-model="newBook.author" type="text" name="author" /></div>
            
            <div><label for="year">Year:</label>
            <input v-model="newBook.year" type="number" name="year" /></div>
            <button type="submit">Vegedvan</button>

            
        </form>
        



        <table>
            <thead class="">
                <th>Azonosito</th>
                <th>Cim</th>
                <th>Szerzo</th>
                <th>Megjelenes</th>
                <th>Muvelet</th>
            </thead>
            <tbody class="">
                <tr v-for="book in books" :key="book.id" class="">
                    <td class="">{{ book.id }}</td>
                    <td class="">{{ book.title }}</td>
                    <td class="">{{ book.author }}</td>
                    <td class="">{{ book.year }}</td>
                    <td class="">
                        <button @click="removeBook(book.id)" type="button">Torles</button>
                    </td>

                </tr>
            </tbody>
            
        </table>

    </main>
</template>