<script>
  import { paths, modals, contextMenu } from '~helpers/stores';
  import { Settings } from '~components/Modal';

  export let onPathSelect;
  export let onItemClick;

  function onFallbackClick() {
    modals.open({
      component: Settings,
      large: true,
      props: { activePageId: 'user-interface' },
    });
    contextMenu.close();
  }
</script>

{#await paths.init()}
  <li>Loading paths...</li>
{:then}
  {#if $paths.length}
    {#each $paths as path}
      <li on:click="{onItemClick(onPathSelect, [path])}">{path}</li>
    {/each}
  {:else}
    <li on:click="{onFallbackClick}">
      No common paths configured yet, click here to add some.
    </li>
  {/if}
{/await}
