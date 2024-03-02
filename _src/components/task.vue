<template>
  <div class="task">
    <h4>task {{ index + 1 }}</h4>
    <p class="date">{{ obj.date }}</p>

    <!--  -->
    <div class="addInput" v-if="obj.edit">
      <input v-model="newTitle" />
      <button v-on:click="addNewTitle(obj)">
        <ion-icon name="checkmark-outline"></ion-icon>
      </button>
    </div>
    <p v-else class="title">{{ obj.title }}</p>
    <!--  -->

    <div class="edit">
      <button v-on:click="editTitle(obj)">
        <ion-icon name="create-outline"></ion-icon>
      </button>
      <button v-on:click="deleteTask(obj)">
        <ion-icon name="trash-outline"></ion-icon>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "task",
  data() {
    return {
      newTitle: "",
    };
  },
  methods: {
    deleteTask: function (objDelete) {
      this.$emit("delete", objDelete);
    },
    editTitle: function (objEdit) {
      objEdit.edit = !objEdit.edit;
      this.newTitle = objEdit.title;
      console.log("objEdit:", objEdit.edit);
    },
    addNewTitle: function (objAdd) {
      objAdd.title = this.newTitle;
      objAdd.edit = !objAdd.edit;
      this.newTitle = "";
    },
  },
  props: {
    obj: Object,
    index: Number,
  },
};
</script>

<style>
.task {
  text-align: left;
  border: 3px solid rgb(4, 170, 109);
  border-radius: 5px;
  background-color: rgb(217, 238, 225);
  padding: 6px;
  margin-bottom: 12px;
}
.task h4 {
  margin: 0;
}
.task p {
  margin: 6px 0;
}
.date {
  color: rgb(102, 95, 95);
  font-size: 13px;
}
.title {
  word-wrap: break-word;
}
.addInput {
  display: flex;
  justify-content: space-between;
}
.addInput input {
  border: none;
  outline: none;
  border-radius: 3px;
  width: 165px;
}
.addInput button {
  outline: none;
  border: none;
  background-color: rgb(4, 170, 109);
  padding: 2px;
  border-radius: 2px;
  display: flex;
}
.addInput button:hover {
  box-shadow: 2px 2px;
}
.edit {
  text-align: center;
}
.edit button {
  padding: 0;
  background-color: rgb(217, 238, 225);
  border: none;
  outline: none;
  margin: 0 10px;
  font-size: larger;
}
</style>
