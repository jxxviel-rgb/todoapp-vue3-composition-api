<template>
  <ul class="list-group">
    <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
      <div class="row">
        <div class="col">
          <span v-if="todo.isDone">
            <del>{{ todo.activity }}</del>
          </span>
          <span v-else>
            <span>{{ todo.activity }}</span>
          </span>
        </div>
        <div class="col-auto">
          <div class="row gx-2">
            <div class="col">
              <button
                @click="deleteAct(index)"
                type="button"
                class="btn btn-danger mx-auto"
              >
                X
              </button>
            </div>
            <div class="col">
              <span v-if="todo.isDone">
                <button
                  @click="undoneAct(index)"
                  type="button"
                  class="btn btn-success mx-auto"
                >
                  Undone
                </button>
              </span>
              <span v-else>
                <button
                  @click="doneAct(index)"
                  type="button"
                  class="btn btn-success mx-auto"
                >
                  Done
                </button>
              </span>
            </div>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  setup(props, { emit }) {
    const deleteAct = (index) => {
      emit("deleteAct", index);
    };

    const doneAct = (index) => {
      emit("doneAct", index);
    };

    const undoneAct = (index) => {
      emit("undoneAct", index);
    };

    return {
      deleteAct,
      doneAct,
      undoneAct,
    };
  },
};
</script>