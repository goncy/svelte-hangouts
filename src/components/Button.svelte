<script>
  import Icon from "svelte-awesome";
  import * as icons from "svelte-awesome/icons";

  export let isActive = false;
  export let icon;
</script>

<style>
  button {
    width: 64px;
    height: 64px;
    background: orangered;
    color: white;
    border-radius: 50%;
    border: none;
    transition: background-color 0.25s linear;
  }

  button:not(:first-of-type) {
    margin-left: 12px;
  }

  button.active {
    background: #fafafa;
    color: #333;
  }
</style>

<button on:click class:active={isActive}>
  <Icon data={icons[icon]} scale={1.5} />
</button>
