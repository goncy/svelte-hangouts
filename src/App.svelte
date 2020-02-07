<script>
  import {onMount} from "svelte";

  import Button from "./components/Button.svelte";
  import User from "./components/User.svelte";

  let video = null;
  let voice = false;

  function toggleVideo() {
    if (video) {
      video.getTracks().map((track) => track.stop());
      video = null;

      return video;
    }

    if (navigator.mediaDevices.getUserMedia) {
      return navigator.mediaDevices
        .getUserMedia({video: true})
        .then(function(_video) {
          video = _video;
        })
        .catch(function(error) {
          console.log("Something went wrong!");
        });
    }
  }

  onMount(toggleVideo);
</script>

<style>
  main {
    display: flex;
    height: 100%;
    position: relative;
  }

  section {
    flex: 1;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  aside {
    position: absolute;
    right: 8px;
    top: 8px;
    display: flex;
    flex-direction: column;
    width: 240px;
  }

  footer {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 64px;
    width: 100%;
    bottom: 8px;
    left: 0;
  }
</style>

<main>
  <section>
    <User {video} name="goncy" />
  </section>
  <aside>
    <User name="fec" />
    <User name="mjs" />
  </aside>
  <footer>
    <Button on:click={() => (voice = !voice)} isActive={voice} icon="microphone" />
    <Button on:click={toggleVideo} isActive={video} icon="videoCamera" />
  </footer>
</main>
