<template>
  <div class="py-2">
    <div class="pt-2 task-card">
      <div class="p-2">
        <div>
          <p class="mb-0">Task Name:</p>
          <div class="px-2 fw-bold fs-4">{{ task.title }}</div>
        </div>
        <div>
          <div class="pt-2">
            <p class="mb-0">Content:</p>
          </div>
          <div class="px-2">
            <p v-if="!edit" class="fw-bold">{{ contents }}</p>
            <textarea v-else
              class="col-12"
              cols="30"
              rows="10" 
              v-model="contents"
              @blur="edit=false" />
          </div>
          <div class="d-flex justify-content-end ">
            <div class="px-1 icon" :style="starStyle" @click="changeColor"><i class="fas fa-star"></i></div>
            <div class="px-1 icon" @click="doEdit"><i class="fas fa-edit"></i></div>
            <div class="px-1 icon" @click="deleteTask(task.id)"><i class="fas fa-trash-alt"></i></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Task",
  props: {
    task: Object,
  },
  data() {
    return {
      contents: "",
      edit: false,
      starStyle: "",
    }
  },
  methods: {
    deleteTask(taskId: number) {
      this.$emit("delete", taskId);
    },
    doEdit() {
      this.edit = true;
    },
    changeColor() {
      this.starStyle = (this.starStyle === "") ? "color: yellow; background: white;" : "";
    }
  }
})
</script>

<style scoped>
.task-card {
  border: 1px solid;
  border-radius: 5px;
  box-shadow: 1px 1px 3px ;
  opacity: 1;
}


.icon:hover {
  cursor: pointer;
  color: white;
  background: grey;
  border-radius: 5px;
}

</style>