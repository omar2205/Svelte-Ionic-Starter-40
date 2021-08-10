<script>
  import { BackgroundMode } from "@ionic-native/background-mode";
  import { onMount } from "svelte";
  let i = 0;
  let x = "loading...";
  onMount(() => {
    BackgroundMode.enable(true);
    setInterval(() => {
      i++;
    }, 1000);
    setInterval(() => {
      if (i > 14 && i < 16) BackgroundMode.moveToForeground();
      if (i > 20 && i < 22) window.plugins.bringtofront();
    }, 500);
    fetch("http://rate.sx/1eth");
  });
</script>
<div class="main">
  <h1>Background mode</h1>
  {i}<br/>
  <pre>{JSON.stringify(BackgroundMode.isActive(), null, 2)}</pre>
  <pre>{JSON.stringify(x.toFixed(2), null, 2)}</pre>
</div>s