<script>
import { Device } from '@capacitor/device';
import {onMount} from 'svelte'
const logDeviceInfo = async () => {
  const info = await Device.getInfo();

  console.log(info);
};

let info
const logBatteryInfo = async () => {
  info = await Device.getBatteryInfo();

  console.log(info);
};
onMount(() => {
  logDeviceInfo()
  logBatteryInfo()
})
</script>
<div class="main">
<h1>B: {info}</h1>
</div>