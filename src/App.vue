<template>
  <div class="container" style="margin-top: 20px">
    <div class="card shadow">
      <div class="card-body">
        <div class="card-title">Simple Todo-list App</div>
        <form>
          <div class="input-group mb-3">
            <input
              @keyup.enter.prevent="add"
              v-model="todo"
              type="text"
              class="form-control"
              placeholder="Mau ngapain?"
              aria-label="Mau ngapain?"
              aria-describedby="button-addon2"
            />
            <button
              @click="add"
              class="btn btn-warning"
              type="submit"
              id="button-addon2"
              data-mdb-ripple-color="dark"
            >
              Add
            </button>
          </div>
        </form>
        <list
          :todos="list"
          @deleteAct="deleteAct"
          @doneAct="doneAct"
          @undoneAct="undoneAct"
        />
        <small>Total Todo : {{ totalTodo }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, toRefs, reactive, onMounted, computed } from "vue";
import List from "./components/List.vue";
export default {
  components: { List },
  setup() {
    const todo = ref("");
    const todos = reactive({
      list: [],
    });

    onMounted(() => {
      const items = localStorage.getItem("todos");
      todos.list = items ? JSON.parse(items) : [];
    });

    const totalTodo = computed(() => {
      return todos.list.length;
    });

    const add = () => {
      todos.list.unshift({ activity: todo.value, isDone: false });
      todo.value = "";
      saveToLocal();
    };

    const deleteAct = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      saveToLocal();
    };

    const doneAct = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true;
        }

        if (!item.isDone) {
          item.isDone != item.isDone;
        }
        return item;
      });
      saveToLocal();
    };

    const undoneAct = (todoIndex) => {
      todos.list = todos.list.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = false;
        }
        if (!item.isDone) {
          item.isDone != item.isDone;
        }

        return item;
      });
      saveToLocal();
    };
    const saveToLocal = () => {
      localStorage.setItem("todos", JSON.stringify(todos.list));
    };

    return {
      todo,
      ...toRefs(todos),
      totalTodo,
      add,
      deleteAct,
      doneAct,
      undoneAct,
    };
  },
};
</script>


