<template>
  <section class="add-todo">
    <form @submit.prevent="addTodo" class="add-todo__form" v-if="isFormVisible">
      <button class="close-button" type="button" @click="closeForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button class="add-todo__show-form-button" v-else @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
interface State {
  isFormVisible: boolean;
  todoText: string;
}
import { Todo } from "@/types/Todo";
import { defineComponent } from "vue";

export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: "",
    };
  },
  methods: {
    showForm() {
      this.isFormVisible = true;
    },
    closeForm() {
      this.isFormVisible = false;
    },
    addTodo() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        complited: false,
      });

      this.todoText = "";
    },
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
});
</script>
