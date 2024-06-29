<script>
  import Header from "$lib/Header.svelte";

  let books = [];
  // array to hold the list of books
  function addBook() {
    books = [...books, ""];
  }
  // adds the user's input to a list of books

  function removeBook(index) {
    books = [...books.slice(0, index), ...books.slice(index + 1)];
  }
  // removes books from the array

  function saveBooks() {
    localStorage.books = JSON.stringify(books);
  }

  function loadBooks() {
    books = JSON.parse(localStorage.books);
  }

  function confirmLoadBooks() {
    var userConfirmed = confirm("are you sure");
    if (userConfirmed) {
      loadBooks();
    } else {
      console.log("cancelled");
    }
  }
</script>

<Header />

<main>
  <button on:click={addBook}>new</button>

  {#each books as book, index}
    <!-- iterates over each book in the array -->
    <div class="book">
      <input bind:value={books[index]} />
    </div>

    <button
      on:click={() => {
        removeBook(index);
      }}>remove</button
    >

    <button
      on:click={() => {
        saveBooks(index);
      }}>save</button
    >

    <button on:click={confirmLoadBooks}>load</button>
  {/each}
</main>

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>
