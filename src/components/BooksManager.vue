<script setup>
import { getBooks } from '../api/books';


</script>
<script>
    export default{
        name: "BooksManager",
        data(){
            return{
                books: [],
            };
        },
        methods:{
            async loadbooks(){
                this.books = await getBooks();
            },
        },
        mounted(){
            this.loadbooks();
        }
    };
</script>
<template>
    <main class="">
        <h1>Konyvtar Kezelo</h1>

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
                    <td class=""{{ book.title }}></td>
                    <td class="">{{ book.author }}</td>
                    <td class="">{{ book.year }}</td>
                    <td class="">-</td>

                </tr>
            </tbody>
            
        </table>

    </main>
</template>