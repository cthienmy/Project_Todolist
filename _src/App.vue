<template>
  <div class="border1">
    <div class="border2">
      <div class="header">
        <h2>TODO App</h2>
        <div class="createTitle">
          <input v-model="title" />
          <button v-on:click="addTask($event)" v-bind:disabled="title === ''">
            <ion-icon name="add-outline"></ion-icon>
          </button>
        </div>
      </div>
      <!--  -->
      <div class="containerTask">
        <h3>Tasks</h3>
        <!--  -->
        <div class="tasks">
          <task
            v-for="(obj, index) in arrTask"
            v-bind:key="index"
            v-bind:obj="obj"
            v-bind:index="index"
            v-on:delete="deleteT($event)"
          />
        </div>
        <!--  -->
      </div>
    </div>
  </div>
</template>
<script>
import task from "./components/task.vue";

export default {
  name: "app",
  data() {
    return {
      arrTask: [],
      title: "",
      date: "",
      edit: false,
    };
  },
  methods: {
    addTask: function (event) {
      this.arrTask.push({
        title: this.title,
        date:
          new Date().getDate() +
          "-" +
          (new Date().getMonth() + 1) +
          "-" +
          new Date().getFullYear(),
        edit: this.edit,
      });
      this.title = "";
    },
    deleteT: function (objDelete) {
      let newArrTask = [];
      this.arrTask.forEach((obj) => {
        if (obj !== objDelete) {
          newArrTask.push(obj);
        }
      });
      this.arrTask = newArrTask;
    },
  },
  components: {
    task,
  },
};
</script>

<style>
.border1 {
  border: 4px solid rgb(4, 170, 109);
  border-bottom: 0px;
  border-right: 0px;
  padding: 4px 0 0 4px;
  border-radius: 15px;
}
.border2 {
  border: 5px solid rgb(4, 170, 109);
  border-bottom: 4px solid rgb(4, 170, 109);
  border-radius: 8px 8px 6px 4px;
  padding: 15px;
  width: 230px;
  height: 430px;
}
.header {
  text-align: left;
}
.header h2 {
  font-weight: 400;
  margin: 0 0 15px;
}
.createTitle {
  background-color: rgb(217, 238, 225);
  padding: 5px;
  display: flex;
  justify-content: space-between;
  border-radius: 5px;
}
.createTitle input {
  width: 170px;

  background-color: rgb(217, 238, 225);
  border: 1px solid rgb(4, 170, 109);
  border-radius: 2px;
  outline: none;
}
.createTitle button {
  padding: 0;
  width: 20px;
  display: flex;
  justify-content: center;
  border-radius: 3px;
  font-size: 20px;
  border: none;
  outline: none;
  background-color: rgb(4, 170, 109);
}
.createTitle button:hover {
  box-shadow: 2px 2px;
}

.containerTask h3 {
  font-weight: 500;
  margin: 13px 0;
}
.tasks {
  height: 290px;
  overflow-y: auto;
}
</style>
