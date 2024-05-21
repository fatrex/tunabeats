<script>
  import BurgerIcon from '~icons/iconamoon/menu-burger-horizontal-duotone';
  import Player from '$lib/components/Player.svelte';
  import Sidebar from '$lib/components/Sidebar.svelte';
  import MobilePlayer from '$lib/drawers/MobilePlayer.svelte';
  import MobileSidebar from '$lib/drawers/MobileSidebar.svelte';
  import '../app.css';
  import {
    AppShell,
    AppBar,
    initializeStores,
    Drawer,
    getDrawerStore,
  } from '@skeletonlabs/skeleton';

  initializeStores();
  const drawerStore = getDrawerStore();

  const openMobileSidebar = () => {
    drawerStore.open({
      id: 'mobile-sidebar',
      position: 'left',
      width: 'w-[80%]',
    });
  };
</script>

<Drawer>
  {#if $drawerStore.id === 'mobile-player'}
    <MobilePlayer />
  {/if}

  {#if $drawerStore.id === 'mobile-sidebar'}
    <MobileSidebar />
  {/if}
</Drawer>

<AppShell>
  <svelte:fragment slot="sidebarLeft">
    <!-- Hidden below Tailwind's large breakpoint -->
    <div id="sidebar-left" class="hidden lg:block">
      <Sidebar />
    </div>
  </svelte:fragment>
  <AppBar class="lg:hidden">
    <svelte:fragment slot="lead">
      <button type="button" on:click={openMobileSidebar}>
        <BurgerIcon />
      </button>
    </svelte:fragment>
  </AppBar>

  <slot />
  <svelte:fragment slot="footer">
    <Player />
  </svelte:fragment>
</AppShell>
