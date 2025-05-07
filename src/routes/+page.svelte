<script>
  import { onMount } from "svelte";

  onMount(() => {
    
  })

  let history = [
    "test1",
    "test2"
  ]

  

  function changeName(name) {
    localStorage
  }
</script>

<div class="terminal">
  {#each history as command}
  {command}
  <br/>
  {/each}
  <p class="field">username@tools:~$</p>
  <span class="cursor"></span>
</div>
<style>

  :global(body){
    background-color: #000;
    color: #ffff;
    font-family: 'Cascadia Code', Consolas, 'Courier New', monospace;
    font-size: 16px;
  padding: 20px;
  white-space: pre-wrap;
}

.field {
  margin: 0;
}

.cursor {
  display: inline-block;
  width: 8px;
  height: 2px;
  background-color: #fff;
  vertical-align: bottom;
  animation: blink 1s steps(1) infinite;
  margin-left: 2px;
}

@keyframes blink {
  0%, 49% {
    opacity: 1;
  }
  50%, 100% {
    opacity: 0;
  }
}

</style>