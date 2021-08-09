<script>
  import { IonicShowModal } from "@utils/IonicHelper";
  import Modal from "@components/Modal.wc.svelte"
  import { Device } from '@capacitor/device'
  import {onMount} from 'svelte'
  let bat
  const logBatteryInfo = async () => {
    bat = await Device.getBatteryInfo()
  }
  onMount(() => {
    logBatteryInfo()
  })
  const showModal = () => {
    IonicShowModal("modal-extra", Modal, {
      firstName: "Douglas",
      lastName: "Adams",
      middleInitial: "N",
    }).then(console.log);
  };
</script>

<div class="main">
  <h5>Welcome to <br/><br/><h3>Svelte with <br/>Ionic + Capacitor!</h3></h5>
  <h1><pre>BAT    {bat * 100}%</pre></h1>
  <ion-button on:click={showModal}>Open Modal</ion-button>
</div>

<style>
  .main {
    text-align: center;
    margin: 50px auto;
  }
</style>
