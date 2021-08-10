<script>
  import { BackgroundMode } from "@ionic-native/background-mode";
  import { onMount } from "svelte";
  let i = 0;
  onMount(() => {
    console.log(BackgroundMode);
    BackgroundMode.enable(true);
    setInterval(() => {
      i++;
    }, 1000);
    setInterval(() => {
      if (i > 20 && i < 25) BackgroundMode.moveToForeground();
    }, 500);
    console.log(BackgroundMode);
  });
</script>
<div class="main">
  <h1>Background mode</h1>
  {i}<br/>
  <pre>{JSON.stringify(BackgroundMode.isActive(), null, 2)}</pre>
</div>