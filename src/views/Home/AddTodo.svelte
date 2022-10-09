<script lang="ts" setup>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let todoMsg: string;
  const add = () => {
    if (todoMsg) {
      dispatch("addTodo", {
        msg: todoMsg,
        done: false,
        id: Date.now(),
      });
      todoMsg = "";
    }
  };
</script>

<div class="flex mb-2">
  <input
    bind:value={todoMsg}
    type="text"
    class="
        w-full
        rounded-l-lg
        border-l-2 border-y-2 border-indigo-300
        pl-4
        focus:outline-indigo-500 focus:outline-none focus:outline-offset-0
      "
    placeholder="請輸入你的代辦事項"
  />
  <button
    class="
        w-[50px]
        h-[50px]
        border-0
        bg-sky-500
        hover:bg-sky-600
        rounded-r-lg
        text-white
        transition
        duration-700
      "
    on:click={add}
  >
    +
  </button>
</div>
