<script lang="ts">
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let lists = [];
</script>

{#if lists.length}
  <ul>
    {#each lists as { msg, done, id } (id)}
      <li
        class="py-4 flex items-center justify-between"
      >
        <label class="text-2xl flex items-center">
          <input
            bind:checked={done}
            type="checkbox"
            class="w-[30px] h-[20px]"
            on:change={() =>
              dispatch("updateDone")}
          />
          <span
            class:line-through={done}
            class:text-gray-400={done}
            >{msg}
          </span>
        </label>
        <span
          class="cursor-pointer text-xl"
          on:click={() =>
            dispatch("deleteItem", id)}
          >❎
        </span>
      </li>
    {/each}
  </ul>
{:else}
  <div
    class="py-10 text-xl font-bold text-center"
  >
    無資料
  </div>
{/if}
