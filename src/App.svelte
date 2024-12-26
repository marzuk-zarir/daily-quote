<script lang="ts">
  const data = $state({
    quote: "",
    author: "",
    isLoading: true,
  })

  $effect(() => {
    (async () => {
      try {
        const res = await fetch('https://dummyjson.com/quotes/random')
        const resData = await res.json()

        data.quote = resData.quote
        data.author = resData.author
        data.isLoading = false
      } catch(e) {
        console.log(e)
        alert("Something went wrong. Try again later...")
      }
    })()
  })
</script>

<main class="bg-emerald-800 w-screen h-screen text-white flex items-center justify-center">
  <div class="mx-20">
    {#if !data.isLoading}
      <h1 class="text-2xl text-justify">"{data.quote}"</h1>
      <p class="text-xl text-right mt-5"> -- {data.author}</p>
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
</main>