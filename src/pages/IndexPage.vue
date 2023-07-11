<template>
  <q-page padding>
    <h3>Todo List</h3>

    <div>
      <q-input label="Title" v-model="newTodo.title">
        <template #prepend>
          <q-input label="Id" v-model="newTodo.id"></q-input>
        </template>
        <template #append>
          <q-checkbox label="Done" v-model="newTodo.done"></q-checkbox>
          <q-btn
            color="primary"
            round
            size="md"
            @click="list.push({ ...newTodo })"
            >Add</q-btn
          >
        </template>
      </q-input>

      <q-list bordered>
        <q-item v-for="item in list" :key="item.id">
          <q-item-section>
            <q-input v-model="item.title" readonly>
              <template #prepend>
                <q-label>#{{ item.id }}</q-label>
                <q-checkbox v-model="item.done" disabled ></q-checkbox>
              </template>
              <template #append>
                <q-btn
                  round
                  color="negative"
                  size="ls"
                  icon="remove"
                  @click="deleteItem(item)"
                ></q-btn>
                <q-btn
                  round
                  color="info"
                  size="ls"
                  icon="edit"
                  @click="editItem(item)"
                ></q-btn>
              </template>
            </q-input>
          </q-item-section>
        </q-item>
      </q-list>

      <q-input
        label="Title"
        v-model="editTodo.title"
        v-if="selectedTodo && editTodo"
      >
        <template #prepend>
          <q-input label="Id" v-model="editTodo.id" readonly></q-input>
        </template>
        <template #append>
          <q-checkbox label="Done" v-model="editTodo.done"></q-checkbox>
          <q-btn color="primary" rounded size="md" @click="updateTodo"
            >Update</q-btn
          >
        </template>
      </q-input>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';

type Todo = {
  id: number;
  title: string;
  done: boolean;
};

const list = ref<Todo[]>([]);

const newTodo = ref<Todo>({
  id: 0,
  title: 'asghar',
  done: false,
});

const deleteItem = (item: Todo) => {
  list.value = list.value.filter((x: Todo) => x.id !== item.id);
};

const editTodo = ref<Todo | undefined>();
const selectedTodo = ref<Todo | undefined>();
const editItem = (item: Todo) => {
  selectedTodo.value = item;
  editTodo.value = { ...item };
};
const updateTodo = () => {
  if (!editTodo.value || !selectedTodo.value) {
    return;
  }
  selectedTodo.value.title = editTodo.value.title;
  selectedTodo.value.done = editTodo.value.done;


  editTodo.value = {id: 0, title: '', done: false}
  selectedTodo.value = undefined;
};
</script>
