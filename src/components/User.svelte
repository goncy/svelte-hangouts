<script>
  export let name = "";
  export let video = null;

  function getRandomColor() {
    const letters = "23456789".split("");
    let color = "#";

    for (var i = 0; i < 6; i++) {
      color += letters[Math.round(Math.random() * (letters.length - 1))];
    }

    return color;
  }

  let element;
  let color = getRandomColor();

  $: initial = name.slice(0, 1).toUpperCase();
  $: video, element, video && element && (element.srcObject = video);
</script>

<style>
  .container {
    min-height: 160px;
    width: 100%;
    height: 100%;
    background: black;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #222;
  }

  .container:not(:first-of-type) {
    margin-top: 8px;
  }

  video {
    height: 100%;
    width: 100%;
  }

  .avatar {
    max-width: 128px;
    max-height: 128px;
    min-width: 96px;
    min-height: 96px;
    height: 20%;
    width: 20%;
    border-radius: 50%;
    color: white;
    font-size: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>

<div class="container">
  {#if video}
    <video autoplay bind:this={element} />
  {:else}
    <div class="avatar" style="background-color: {color}">{initial}</div>
  {/if}
</div>
