<script lang="ts">
  import { Avatar, RangeSlider } from '@skeletonlabs/skeleton';
  import { isPlaying } from '$lib/stores/player';
  import PlayIcon from '~icons/iconamoon/player-play-duotone';
</script>

{#if $isPlaying}
  <div class="mini-player">
    <div class="media">
      <div class="cover">
        <Avatar
          src="https://www.altpress.com/wp-content/uploads/2024/02/29/Twenty-One-Pilots-Clancy-Album-Art-LO-1.jpg"
          rounded="rounded-2xl"
          shadow="shadow-md"
          border="border"
        />
      </div>
      <div class="title">
        <p class="artist">Twenty One Pilots</p>
        <p class="track">Overcompensate</p>
      </div>
      <div class="buttons">
        <PlayIcon />
      </div>
    </div>
    <div class="progress">
      <RangeSlider name="seekbar" accent="accent-surface-500" />
    </div>
  </div>
{/if}

<style lang="postcss">
  .mini-player {
    @apply h-28 bg-secondary-500 px-2 py-3;

    .media {
      @apply flex flex-row h-[75px];

      .cover {
        @apply w-3/12;
        @apply flex items-center justify-center;
        @apply bg-no-repeat bg-cover bg-center;
        @apply h-full;
      }

      .title {
        @apply w-7/12 h-full;
        @apply flex flex-col justify-center text-white text-sm;

        .track {
          @apply font-semibold;
        }
      }

      .buttons {
        @apply w-auto flex items-center text-white text-4xl h-full;
      }
    }

    .progress {
      @apply h-[25px] w-full;
    }
  }
</style>
