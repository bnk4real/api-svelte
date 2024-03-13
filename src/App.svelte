<script>
  import "mdb-ui-kit/css/mdb.min.css";
  import Navbar from "../components/Navbar.svelte";
  import Footer from "../components/Footer.svelte";

  let data = [];

  async function fetchData() {
    try {
      const headers = new Headers();
      // Set Headers
      // headers.append("Content-Type", "application/json");
      // headers.append("request-id", `${new Date().toISOString()}`);
      // headers.append("caller-id", "caller 123");
      // headers.append("application-channel", "test");
      // headers.append("transaction-dateTime", new Date().toISOString());
      // headers.append("x-user-info", "{{xuserinfo}}");
      const response = await fetch("https://www.melivecode.com/api/users", {
        // Change the method as per your API requirements (GET, POST, etc.)
        method: "GET",
        headers: headers,
      });

      if (!response.ok) {
        throw new Error("Cannot call API");
      }

      data = await response.json();
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  }

  fetchData();
</script>

<main>
  <Navbar />

  <div class="container">
    <!-- Check if resp data from API is not null -->
    {#if data.length === 0}
      <p>Loading...</p>
    {:else}
      <!-- loop data through list -->
      <ul class="list-group list-group-light mt-5">
        {#each data as user}
          <li class="list-group-item" key={user.id}>
            <h3>ID : {user.id}</h3>
            <h3>Firstname : {user.fname}</h3>
            <h3>Lastname : {user.lname}</h3>
            <h3>Username : {user.username}</h3>
          </li>
        {/each}
      </ul>
    {/if}
  </div>

  <Footer />
</main>
