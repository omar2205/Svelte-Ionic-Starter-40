<script>
  import { IonicShowModal } from "@utils/IonicHelper";
  import Modal from "@components/Modal.wc.svelte";
  import { Device } from "@capacitor/device";
  import { App } from "@capacitor/app";
  import { Toast } from "@capacitor/toast";
  import { BackgroundTask } from "@robingenz/capacitor-background-task";

  import { onMount } from "svelte";
  let bat;
  let i = 0;
  const logBatteryInfo = async () => {
    let b = await Device.getBatteryInfo();
    bat = ((await b.batteryLevel) * 100).toFixed(2);
    await Toast.show({
      text: "Hey"
    });
  };
  onMount(() => {
    logBatteryInfo();
    App.addListener("appStateChange", async ({ isActive }) => {
      if (isActive) {
        return;
      }
      // The app state has been changed to inactive.
      // Start the background task by calling `beforeExit`.
      const taskId = await BackgroundTask.beforeExit(async () => {
        setInterval(() => {
          i++;
          if (i === 30) async () => await Toast.show({ text: "i is 30" });
        }, 1000);
        // BackgroundTask.finish({ taskId });
      });
    });
  });
  const showModal = () => {
    IonicShowModal("modal-extra", Modal, {
      firstName: "Douglas",
      lastName: "Adams",
      middleInitial: "N"
    }).then(console.log);
  };
</script>

<div class="main">
  <h5>Welcome to <br/><br/><h3>Svelte with <br/>Ionic + Capacitor!</h3></h5>
  <h1><pre>BAT    <b>{bat}%</b></pre></h1>
  {i}<br/>
  <ion-button expand="block" on:click={showModal}>Open Modal</ion-button>
</div>

<style>
  .main {
    text-align: center;
    margin: 50px auto;
  }
</style>
