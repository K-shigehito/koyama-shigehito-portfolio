<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { externalLinks, pageLinks } from '@library/linkData';
  import IconClose from '@components/icons/IconClose.svelte';
  import IconArrowTopRightOnSquare from '@components/icons/IconArrowTopRightOnSquare.svelte';

  export let dialog: HTMLDialogElement;
  export let currentPage: string;

  const dispatch = createEventDispatcher();
  const clickClose = () => {
    dispatch('closeDialog');
  };
</script>

<dialog
  bind:this={dialog}
  class="absolute top-4 bottom-auto right-4 left-auto overflow-y-auto rounded-md bg-slate-50 shadow-md backdrop:bg-slate-900/20 backdrop:backdrop-blur-sm"
>
  <div
    class="grid grid-cols-1 grid-rows-1 items-start justify-items-end px-4 pt-6 pb-3"
  >
    <button
      type="button"
      on:click={clickClose}
      class="z-10 col-start-1 row-start-1 -mr-5 -mt-8 rounded-md px-2 py-2 text-sm text-slate-700 hover:text-slate-900"
    >
      <span class="sr-only">閉じる</span>
      <IconClose />
    </button>

    <nav class="col-start-1 row-start-1">
      <ul
        class="flex flex-col gap-4 font-barlow text-2xl font-semibold leading-8 tracking-widest"
      >
        <div class="flex flex-col gap-4">
          {#each pageLinks as link (link.label)}
            {#if link.label === currentPage.toUpperCase()}
              <li>
                <a
                  class="flex items-center gap-4 before:block before:h-2 before:w-2 before:shrink-0 before:rounded-full before:bg-teal-500"
                  href={link.href}>{link.label}</a
                >
              </li>
            {:else}
              <li>
                <a
                  class="flex items-center gap-4 text-slate-500 duration-150 before:block before:h-2 before:w-2 before:shrink-0 before:rounded-full before:bg-slate-400 hover:text-slate-900"
                  href={link.href}>{link.label}</a
                >
              </li>
            {/if}
          {/each}
        </div>

        <div
          class="mt-2 flex gap-6 border-t border-t-slate-300 px-1 pt-4 font-barlow-semi text-lg font-semibold tracking-wide text-slate-600 duration-150 hover:text-slate-900"
        >
          {#each externalLinks as externalLink (externalLink.label)}
            <li>
              <a href={externalLink.href} class="flex items-center gap-1">
                {externalLink.label}
                <span>
                  <IconArrowTopRightOnSquare />
                </span>
              </a>
            </li>
          {/each}
        </div>
      </ul>
    </nav>
  </div>
</dialog>
