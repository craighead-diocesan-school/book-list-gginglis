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
  // saves books to storage

  function loadBooks() {
    books = JSON.parse(localStorage.books);
  }
  // retrieves saved books after refreshing

  function confirmLoadBooks() {
    var userConfirmed = confirm("are you sure");
    // asks the user whether they want to load or not
    if (userConfirmed) {
      loadBooks();
      // loads the books at user's confirmation
    } else {
      console.log("cancelled");
      // cancels the request to load books
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
    <!-- lets the user input a book title -->

    <button
      on:click={() => {
        removeBook(index);
      }}>remove</button
    >
    <!-- removes user's chosen book from the array -->

    <button
      on:click={() => {
        saveBooks(index);
      }}>save</button
    >
    <!-- saves the book to the localStorage -->

    <button on:click={confirmLoadBooks}>load</button>
    <!-- asks the user whether they want to load the books or not, and runs whatever they pick -->
  {/each}
</main>

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>
