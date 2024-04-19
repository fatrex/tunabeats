<script lang="ts">
  import { Avatar, RangeSlider, getDrawerStore } from '@skeletonlabs/skeleton';
  import { isPlaying } from '$lib/stores/player';
  import PlayIcon from '~icons/iconamoon/player-play-duotone';
  import NextIcon from '~icons/iconamoon/player-next-duotone';
  import PrevIcon from '~icons/iconamoon/player-previous-duotone';
  import ArrowUpIcon from '~icons/iconamoon/arrow-up-2-fill';
  import HearthIcon from '~icons/iconamoon/heart-duotone';

  export let size: 'normal' | 'mobile-player' = 'normal';

  const drawerStore = getDrawerStore();

  const openMobilePlayer = () => {
    drawerStore.open({
      id: 'mobile-player',
      position: 'bottom',
      bgDrawer: 'bg-secondary-500',
      height: 'h-[90%]',
    });
  };
</script>

{#if $isPlaying}
  <div class="player" class:mobile-player={size === 'mobile-player'}>
    {#if size !== 'mobile-player'}
      <div class="absolute -top-12 text-secondary-500 text-7xl w-full flex flex-row justify-center">
        <button on:click={() => openMobilePlayer()}>
          <ArrowUpIcon />
        </button>
      </div>
    {/if}
    <div class="media">
      <div class="cover">
        <Avatar
          src="https://www.altpress.com/wp-content/uploads/2024/02/29/Twenty-One-Pilots-Clancy-Album-Art-LO-1.jpg"
          rounded="rounded-2xl"
          shadow="shadow-md"
          border="border"
          width={size === 'mobile-player' ? 'w-auto' : 'w-16'}
        />
      </div>
      <div class="info">
        <div class="">
          <p class="artist">Twenty One Pilots</p>
          <p class="track">Overcompensate</p>
        </div>
        {#if size !== 'normal'}
          <div class="fav">
            <HearthIcon />
          </div>
        {/if}
      </div>
      <div class="buttons">
        {#if size !== 'normal'}
          <PrevIcon />
        {/if}
        <PlayIcon />
        {#if size !== 'normal'}
          <NextIcon />
        {/if}
      </div>
    </div>
    <div class="progress">
      <RangeSlider name="seekbar" accent="accent-surface-500" />
    </div>
  </div>
{/if}

<style lang="postcss">
  .player {
    @apply h-28 bg-secondary-500 px-2 py-3 relative w-full;

    .media {
      @apply flex flex-row h-[75px];

      .cover {
        @apply w-3/12;
        @apply flex items-center justify-center;
        @apply h-full;
      }

      .info {
        @apply w-7/12 h-full;
        @apply flex flex-col justify-center text-white text-sm;

        .track {
          @apply font-semibold;
        }
      }

      .buttons {
        @apply w-auto flex items-center justify-between text-white text-4xl h-full;
      }
    }

    .progress {
      @apply h-[25px] w-full;
    }

    &.mobile-player {
      @apply h-full;
      .media {
        @apply flex flex-col h-[90%];
        .cover {
          @apply w-full h-1/3 flex-grow h-full;
        }
        .info {
          @apply w-full h-60 flex flex-row justify-between items-center;
          .fav {
            @apply text-4xl;
          }
        }
        .button {
        }
      }
    }
  }
</style>
