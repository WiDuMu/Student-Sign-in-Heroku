<template>
  <div>
    <div class="alert alert-danger" v-show="errors.length > 0">
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </div>

    <div class="card add-student m-2 p-2">
      <h4 class="card-title">Add new student</h4>

      <div class="form-group">
        <label for="name">Name</label>
        <!-- TODO v-model newStudentName -->
        <input id="name" class="form-control" v-model.trim="newStudentName" />
      </div>
      <div class="form-group">
        <label for="starID">Star ID</label>
        <!-- TODO v-model newStarID -->
        <input id="starID" class="form-control" v-model.trim="newStarID" />
      </div>
      <!-- TODO v-on:click event handler -->
      <button class="btn btn-primary" v-on:click="addStudent">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NewStudentForm",
  emits: ['student-added'],
  data() {
    return {
      newStudentName: "",
      newStarID: "",
      errors: [],
    };
  },
  methods: {
    addStudent() {
      this.errors = [];
      if (!this.newStudentName) {
        this.errors.push("Must enter student name!");
      }
      if (!this.newStarID) {
        this.errors.push("Must have StarID");
      }
      if (this.errors.length == 0) {
        let newStudent = {
          name: this.newStudentName,
          starID: this.newStarID,
          present: false,
        };
        this.$emit('student-added', newStudent);
        this.newStudentName = "";
        this.newStarID = "";
      }
    },
  },
};
</script>
<style scoped>
</style>