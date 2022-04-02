<template>

  <div class="card student-list m-2 p-2">
    <h4 class="card-title">Student List</h4>
    <div id="student-table">
      <table class="table">
        <tr>
          <th>Name</th>
          <th>StarID</th>
          <th>Present?</th>
        </tr>
        <tr v-for="student in students" v-bind:class="{present: student.present, absent: !student.present}">
          <td>{{student.name}}</td>
          <td>{{student.starID}}</td>
          <td>
            <input type="checkbox" v-bind:checked="student.present" @change="arrivedOrLeft(student,$event.target.checked)">
          </td>
        </tr>

        <!-- TODO create table rows
        Each row will have a checkbox, bound to the app's data
        When the checkbox is checked/unchecked, the student will be signed in/out -->

      </table>
    </div>
  </div>

</template>

<script>
export default {
  name: "StudentTable",
  emits:["student-arrived-or-left"],
  props: {
    students:Array
  },
  methods: {
    arrivedOrLeft(student,present) {
      // emit message to parrent
      this.$emit("student-arrived-or-left",student, present)
    }
  }
}
</script>

<style scoped>

.absent {
  color: lightgray;
  font-style: italic;
  background-color: darkblue;
}

.present {
  color: black;
  font-weight: bold;
  background-color: mediumaquamarine;
}

#student-table {
  max-height: 400px;
  overflow: scroll;
}
</style>