<script>
  import Player from '$lib/components/Player.svelte';
  import MobilePlayer from '$lib/drawers/MobilePlayer.svelte';
  import '../app.css';
  import { AppShell, initializeStores, Drawer, getDrawerStore } from '@skeletonlabs/skeleton';

  initializeStores();
  const drawerStore = getDrawerStore();
</script>

<Drawer>
  {#if $drawerStore.id === 'mobile-player'}
    <MobilePlayer />
  {/if}
</Drawer>

<AppShell>
  <svelte:fragment slot="sidebarLeft">
    <!-- Hidden below Tailwind's large breakpoint -->
    <div id="sidebar-left" class="hidden lg:block">Sidebar</div>
  </svelte:fragment>
  <slot />
  <svelte:fragment slot="footer">
    <Player />
  </svelte:fragment>
</AppShell>
