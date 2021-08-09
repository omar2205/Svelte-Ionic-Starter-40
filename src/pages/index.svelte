<script>
  import { IonicShowModal } from "@utils/IonicHelper";
  import Modal from "@components/Modal.wc.svelte"
  // import * as X from '@ionic-native/battery-status'
  import {BatteryStatus} from '@ionic-native/battery-status'
  
  import { Plugins } from '@capacitor/core'
  const { Device } = Plugins
  
  let bat = '0%'
  let bat2 = '0%'
  let b, c
  
  import {onMount} from 'svelte'
  const loadInfo = async () => {
    b = await Device.getBatteryInfo()
    c = await Device.getInfo()
  }
  onMount(() => {
    loadInfo()
    // console.log(X)
    // setTimeout(() => 
    // , 1000)
    window.BatteryStatus = BatteryStatus
    BatteryStatus.onChange = e => {
      bat = `${e.level}%`
    }
    window.addEventListener("batterystatus", onBatteryStatus, false);

    function onBatteryStatus(e) {
      bat2 = `${e.level}%`
    }
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
  <h1><pre>BAT    {bat}</pre></h1>
  <h1><pre>BAT2   {bat}</pre></h1>
  <h1><pre>XXB    
  {JSON.stringify(b, null, 2)}
  {JSON.stringify(c, null, 2)}</pre></h1>
  <ion-button on:click={showModal}>Open Modal</ion-button>
</div>

<style>
  .main {
    text-align: center;
    margin: 50px auto;
  }
</style>
