<script lang="ts">
  let taskList = $state([{ text: "Tester svelte", status: true }]);
  let newItem = $state("");

  function addToList(event: Event) {
    event.preventDefault();
    if (newItem.trim() !== "") {
      taskList = [...taskList, { text: newItem, status: false }];
      newItem = "";
    }
  }

  function swapStatus(index: number) {
    taskList = taskList.map((task, i) =>
      i === index ? { ...task, status: !task.status } : task
    );
  }
</script>

<div class="flex flex-col justify-center w-full min-h-screen bg-gray-100">
  <h1 class="text-5xl font-semibold text-center py-20">
    To-Do APP <br />
    <span class="inline-flex gap-2 text-3xl font-normal"
      >Make with <img src="/logo.png" alt="logo" class="h-10" /></span
    >
  </h1>
  <div class="w-full flex flex-col items-center">
    <form
      action=""
      class="border-2 border-orange-600 w-fit rounded-sm overflow-hidden bg-white"
      onsubmit={addToList}
    >
      <input
        type="text"
        class="focus:outline-none focus:ring-0 px-3 w-80"
        placeholder="Entrez vos tâches"
        bind:value={newItem}
      />
      <button
        type="submit"
        class="bg-orange-600 text-white py-2 px-3 hover:bg-orange-700 transition-colors"
        >Add Task</button
      >
    </form>
    <div class=" w-150">
      {#each taskList as task, index}
        <div
          class="flex shadow-md mt-6 bg-white items-center gap-2 border-2 border-orange-600 p-8 hover:bg-gray-100 rounded-xl"
        >
          <input
            type="checkbox"
            name="status"
            checked={task.status}
            onchange={() => swapStatus(index)}
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500"
          />
          <p
            class="flex-1 {task.status
              ? 'line-through text-gray-500'
              : 'text-gray-700'}"
          >
            {task.text}
          </p>
          {#if task.status === false}
            <p class="text-red-500">à faire</p>
          {:else}
            <p class="text-green-500">fait</p>
          {/if}
        </div>
      {/each}
    </div>
  </div>
</div>
