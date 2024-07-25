<script>
  import Header from "$lib/Header.svelte";

  let lists = [
    {
      name: "fiction",
      list: [
        { name: "rooftoppers", read: false },
        { name: "the good thieves", read: false },
      ],
    },
    {
      name: "recipe",
      list: [
        { name: "eat", read: false },
        { name: "supergood", read: false },
      ],
    },
  ];
  // array to hold the list of books
  let list = "";

  let current = lists[0];

  function addItem() {
    current.list = [...current.list, { name: "", read: false }];
  }
  // adds the user's input to a list of books

  function removeItem(index) {
    current.list = [
      ...current.list.slice(0, index),
      ...current.list.slice(index + 1),
    ];
  }
  // removes books from the array

  function saveItems() {
    localStorage.items = JSON.stringify(lists);
    alert("saved");
  }
  // saves books to storage

  function loadItems() {
    lists = JSON.parse(localStorage.items);
    alert("loaded");
  }
  // retrieves saved books after refreshing

  function confirmLoadItems() {
    var userConfirmed = confirm("are you sure");
    // asks the user whether they want to load or not
    if (userConfirmed) {
      loadItems();
      // loads the books at user's confirmation
    } else {
      alert("cancelled");
      // suggest using alert here
      // cancels the request to load books
    }
  }
</script>

<Header />

<main>
  <select bind:value={current}>
    {#each lists as list}
      <option value={list}>
        {list.name}
      </option>
    {/each}
  </select>

  <!-- adds input bar -->
  <button on:click={saveItems}>save</button>
  <!-- saves the current list -->
  <button on:click={confirmLoadItems}>load</button>
  <!-- asks the user whether they want to load the books or not, and runs whatever they pick -->

  <!-- Display all of the items in the currently selected list. -->
  {#each current.list as item, index}
    <div class="book">
      <button
        on:click={() => {
          removeItem(index);
        }}>-</button
      >
      <input bind:value={item.name} />
      <input type="checkbox" bind:checked={item.read} />
    </div>
  {/each}
  <button on:click={addItem}>+</button>
  <!-- 
  saves the book to the localStorage
  {#each books as book, index}
    iterates over each book in the array
    <div class="book">
      <input bind:value={books[index].name} />
      <input type="checkbox" bind:checked={books[index].read} />
    </div>
    lets the user input a book title
    <button
      on:click={() => {
        removeBook(index);
      }}>remove</button
    >
    removes user's chosen book from the array
  {/each} -->
</main>

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>

<style>
  main {
    background-color: rgb(191, 230, 191);
    padding: 15px 35px;
  }

  button {
    background-color: rgb(150, 218, 150);
    border: solid rgb(150, 218, 150) 2px;
    border-radius: 12px;
    padding: 2px 7px;
    margin: 3px;
    font-family: "Poppins", sans-serif;
    font-weight: 500;
    color: rgb(16, 37, 16);
  }

  button:hover {
    background-color: rgb(120, 209, 120);
    border: solid rgb(120, 209, 120) 2px;
    transition: 0.25s;
  }

  footer {
    background-color: rgb(191, 230, 191);
    font-family: "Poppins", sans-serif;
    color: rgb(16, 37, 16);
    padding: 30px;
  }

  .book {
    display: flex;
  }

  input {
    height: 22px;
    margin: 5px 2.5px 0px;
  }
</style>
