<script>
  import Header from "$lib/Header.svelte";

  let books = [];
  // array to hold the list of books
  function addBook() {
    books = [...books, ""];
  }
  // adds the user's input to a list of books
</script>

<Header />

<main>
  <button on:click={addBook}>new</button>

  {#each books as book, index}
    <!-- iterates over each book in the array -->
    <div class="book">
      <input bind:value={books[index]} />
    </div>
  {/each}
</main>

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>
