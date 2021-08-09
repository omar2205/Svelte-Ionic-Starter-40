<script lang="typescript">
	import { Router } from "@roxi/routify";
	import { routes } from "../.routify/routes";
</script>

  <ion-app>
    <ion-header translucent>
      <ion-toolbar>
        <ion-title>Battery N30</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content fullscreen class="ion-padding">
			<Router {routes} />
    </ion-content>
  </ion-app>

<style @global>
</style>
