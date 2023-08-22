<script>
  import { onMount } from "svelte";
let users = [];
let loading = true;
async function getUsers() {
    const response = await fetch('https://api.github.com/users');
    return await response.json();
};
</script>

<style>
    h2 {
        text-align: center;
    }
</style>

{#await getUsers()}
  <h2>loading ...</h2>
{:then users} 
  {#each users as user}
    <article class="user">
        <img src={user.avatar_url} alt={user.login} />
        <div class="user-info">
            <h3>User: {user.login}</h3>
            <a href={user.html_url} class="btn-primary" target="_blank">github url</a>
        </div>
    </article>
  {/each}
{:catch error}
    <h2>Something wenr wrong ... {error?.message}</h2>    
{/await}

