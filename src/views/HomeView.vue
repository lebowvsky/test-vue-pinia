<template>
  <div class="home">
    <h1 class="title">My Todo app...</h1>
    <StatisticsComponent />
    <div class="container">
      <div class="tasks-wrapper">
        <h2>Mes tâches</h2>
        <div class="tasks-wrapper">
          <div class="tw-task" v-for="task in tasksStore.tasks" :key="task.id">
            <div class="title-wrapper">
              <input type="checkbox" v-model="task.completed" :id="task.id" />
              <h3>{{ task.title }}</h3>
            </div>
            <p>{{ task.text }}</p>
            <div class="buttons-wrapper">
              <button @click="removeTask(task)" class="remove">
                Effacer tâche
              </button>
              <button
                v-if="!task.completed"
                @click="editTask(task)"
                class="edit"
              >
                Éditer tâche
              </button>
            </div>
          </div>
        </div>
      </div>
      <FormComponent />
    </div>
  </div>
</template>

<script setup lang="ts">
import StatisticsComponent from "@/components/StatisticsComponent.vue";
import FormComponent from "@/components/FormComponent.vue";
import { Task } from "@/definitions/task";
import { useTasksStore } from "@/stores/task";

const tasksStore = useTasksStore();

const removeTask = (task: Task) => {
  tasksStore.removeTask(task.id);
};

const editTask = (task: Task) => {
  tasksStore.selectedTask = task;
  tasksStore.removeTask(task.id);
};
</script>

<style lang="scss" scoped>
.home {
  .container {
    margin: 50px 0;
    width: 100%;
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
    padding: 20px;

    .tasks-wrapper {
      .tw-task {
        background-color: rgb(167, 208, 164);
        border-radius: 10px;
        padding: 10px 20px;
        margin: 15px 0;
        width: 600px;

        .title-wrapper {
          display: flex;

          input {
            margin: 0 10px 0 0;
          }
        }

        button {
          cursor: pointer;
          border: none;
          border-radius: 5px;
          padding: 8px 20px;
          color: white;
          margin-right: 15px;

          &.edit {
            background-color: rgb(108, 97, 204);

            &:hover {
              background-color: rgb(79, 71, 151);
            }
          }
          &.remove {
            background-color: rgb(204, 104, 97);

            &:hover {
              background-color: rgb(154, 78, 73);
            }
          }
        }
      }
    }
  }
}
</style>
