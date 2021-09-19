<script>
  let domain = "<YOUR DOMAIN>";
  let output;
  let name, link;
  async function shortenLink() {
    let res = await fetch(`${domain}`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: name,
        url: link,
      }),
    });
    if (res.ok) {
      output = domain + "/" + name;
    } else {
      alert("Please try again with another name");
    }
  }
</script>

<form
  name="shortenForm"
  class="shortenForm"
  on:click|preventDefault={shortenLink}
>
  <input
    type="text"
    name="name"
    placeholder="Name of the shortened link"
    bind:value={name}
    class="shortenForm__name"
  />
  <input
    type="text"
    name="link"
    placeholder="Link you want to shorten"
    bind:value={link}
    class="shortenForm__link"
  />
  <button>Make it shorter!</button>
  {#if output}
    <br />
    <p>Generated link:</p>
    <a href={output} target="_blank">{output}</a>
  {/if}
</form>

<style>
  .shortenForm {
    width: clamp(200px, 500px, 95vw);
    margin: auto;
    padding: 20px;
    border: 1px solid #e0e0e0;
    border-radius: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .shortenForm__name {
    display: block;
    width: 100%;
  }
  .shortenForm__link {
    display: block;
    width: 100%;
  }
</style>
