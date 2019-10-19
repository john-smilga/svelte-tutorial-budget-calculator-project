<script>
  import { onMount } from "svelte";
  let users = [];
  let loading = true;
  onMount(async () => {
    let userData = await fetch("https://api.github.com/users");
    let githubUsers = await userData.json();
    users = githubUsers;
    loading = false;
  });
</script>

<style>
  h2 {
    text-align: center;
  }
</style>

{#if loading}
  <h2>Loading ...</h2>
{:else}
  <section>
    {#each users as user}
      <article class="user">
        <img src={user.avatar_url} alt="" />
        <div class="user-info">
          <h3>User:{user.login}</h3>
          <a href={user.html_url} class="btn-primary" target="_blank">
            github url
          </a>
        </div>
      </article>
    {/each}
  </section>
{/if}
