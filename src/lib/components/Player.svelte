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
      <div class="expand-player">
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
        <div class="prev-button">
          <PrevIcon />
        </div>
        <div class="play-button">
          <PlayIcon />
        </div>

        <div class="next-button">
          <NextIcon />
        </div>
      </div>
      <div class="progress">
        <RangeSlider name="seekbar" accent="accent-surface-500">
          <div class="timings">
            <div class="current">00:00</div>
            <div class="total">00:00</div>
          </div>
        </RangeSlider>
      </div>
    </div>
  </div>
{/if}

<style lang="postcss">
  .player {
    @apply h-28 bg-secondary-500 px-2 py-3 relative w-full flex-wrap flex flex-row;

    .expand-player {
      @apply absolute -top-12 text-secondary-500 text-7xl w-full flex flex-row justify-center;
      @apply lg:hidden;
    }

    .media {
      @apply flex flex-row h-[75px] flex-wrap;
      @apply sm:w-full;
      @apply lg:flex-nowrap;
      @apply lg:h-full lg:space-x-10;

      .cover {
        @apply w-3/12 h-full;
        @apply flex items-center justify-center;
        @apply sm:w-2/12;
        @apply lg:w-1/12;
      }

      .info {
        @apply w-7/12 h-full;
        @apply flex flex-col justify-center text-white text-sm;
        @apply sm:w-5/12;
        @apply lg:w-2/12;

        .track {
          @apply font-semibold;
        }
      }

      .buttons {
        @apply w-2/12 h-full;
        @apply flex items-center justify-between text-white text-4xl;
        @apply sm:gap-x-6;
        @apply sm:w-5/12;
        @apply lg:order-last lg:text-2xl lg:w-3/12 lg:justify-around;

        .prev-button {
          @apply hidden;
          @apply sm:block;
        }

        .next-button {
          @apply hidden;
          @apply sm:block;
        }
      }

      .progress {
        @apply h-[25px] w-full;
        @apply lg:h-full lg:flex lg:flex-col lg:justify-center lg:w-6/12;
        .timings {
          @apply hidden justify-between text-sm text-white;
          @apply lg:flex lg:flex-row;
        }
      }
    }

    &.mobile-player {
      @apply h-full;
      .media {
        @apply flex flex-col h-[90%] flex-nowrap;
        @apply sm:flex-row sm:flex-wrap;
        .cover {
          @apply w-full flex-grow h-full;
          @apply sm:w-3/12;
        }
        .info {
          @apply w-full h-60 flex flex-row justify-between items-center text-base;
          @apply sm:w-5/12 sm:px-5 sm:pr-14 sm:h-full;
          .fav {
            @apply text-4xl;
          }
        }
        .buttons {
          @apply w-full flex items-center;
          @apply sm:w-4/12;
          .prev-button {
            @apply block;
          }
          .next-button {
            @apply block;
          }
        }
      }
    }
  }
</style>
