<script>
  import { BackgroundMode } from "@ionic-native/background-mode";
  import { onMount } from "svelte";
  onMount(() => {
    console.log(BackgroundMode);
    BackgroundMode.enable(true);
    console.log(BackgroundMode);
  });
</script>
<div class="main">
  <h1>Background mode</h1>
  <pre>{JSON.stringify(BackgroundMode.isActive(), null, 2)}</pre>
</div>