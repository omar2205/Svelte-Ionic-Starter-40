<script>
  const BACKEND_API = "http://192.168.1.99:9000";
  import { onMount } from "svelte";
  import { BackgroundMode } from "@ionic-native/background-mode";
  import { Http } from "@capacitor-community/http";
  let i = 0;
  let x = "loading...";
  // Example of a GET request
  const doGet = async () => {
    const options = {
      url: `${BACKEND_API}/try.txt`
    };

    const res = await Http.get(options);
    x = await res.data;
  };
  onMount(() => {
    BackgroundMode.enable(true);
    setInterval(() => {
      i++;
    }, 1000);
    setInterval(() => {
      if (i > 14 && i < 16) BackgroundMode.moveToForeground();
      if (i > 20 && i < 22) window.plugins.bringtofront();
    }, 500);
    doGet();
  });
</script>
<div class="main">
  <h1>Background mode</h1>
  {i}<br/>
  <pre>{JSON.stringify(BackgroundMode.isActive(), null, 2)}</pre>
  <pre>{JSON.stringify(x, null, 2)}</pre>
</div>