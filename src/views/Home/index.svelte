<script lang="ts">
  import ButtonUtils from "../../components/ButtonUtils.svelte";
  import AddTodo from "./AddTodo.svelte";
  import ListTodo from "./ListTodo.svelte";

  interface TodoItem {
    msg: string;
    done: boolean;
    id: number;
  }
  let tempLists: TodoItem[] = [
    { msg: "打code", done: true, id: 1 },
    { msg: "打遊戲", done: false, id: 2 },
    { msg: "吃飯", done: false, id: 3 },
    { msg: "睡覺", done: false, id: 4 },
  ];
  let lists: TodoItem[];
  let selectStatus: string;

  const selectData = (target: string = "all") => {
    selectStatus = target;
    switch (target) {
      case "all":
        lists = [...tempLists];
        break;
      case "undone":
        lists = [...tempLists].filter(
          (item) => item.done
        );
        break;
      default:
        lists = [...tempLists].filter(
          (item) => !item.done
        );
        break;
    }
  };

  const addTodo = ({
    detail,
  }: {
    detail: TodoItem;
  }) => {
    tempLists.push(detail);
    selectData(selectStatus);
  };

  let hasDone: number;
  const updateDone = () => {
    hasDone = (lists ?? tempLists).filter(
      (item) => item.done
    ).length;
    selectData(selectStatus);
  };
  updateDone();

  const deleteItem = ({
    detail,
  }: {
    detail: number;
  }) => {
    tempLists = tempLists.filter(
      ({ id }) => id !== detail
    );
    selectData(selectStatus);
  };

  const clearHasDone = () => {
    tempLists = tempLists.filter(
      (item) => !item.done
    );
    selectData(selectStatus);
  };

  const clearAll = () => {
    tempLists.length = 0;
    selectData(selectStatus);
  };
</script>

<div
  class="bg-gray-700 p-10 min-h-screen flex justify-center"
>
  <div
    class="max-w-[768px] bg-white p-5 rounded-lg w-full"
  >
    <h1 class="text-center text-2xl mb-4">
      Svelte TypeScript ToDoList
    </h1>
    <AddTodo on:addTodo={addTodo} />
    <div class="text-center">
      <ButtonUtils color="primary">
        <div on:click={() => selectData("all")}>
          全部
        </div>
      </ButtonUtils>
      <ButtonUtils color="primary">
        <div
          on:click={() => selectData("undone")}
        >
          已完成
        </div>
      </ButtonUtils>
      <ButtonUtils color="primary">
        <div
          on:click={() => selectData("completed")}
        >
          未完成
        </div>
      </ButtonUtils>
    </div>
    <ListTodo
      {lists}
      on:updateDone={updateDone}
      on:deleteItem={deleteItem}
    />
    <div
      class="flex justify-between items-center"
    >
      <p>
        目前有 <span class="font-medium"
          >{hasDone}</span
        > 個事項待完成
      </p>

      <div>
        <ButtonUtils color="secondary">
          <div on:click={clearHasDone}>
            清除完成事項
          </div>
        </ButtonUtils>
        <ButtonUtils color="rose">
          <div on:click={clearAll}>全部清除</div>
        </ButtonUtils>
      </div>
    </div>
  </div>
</div>
