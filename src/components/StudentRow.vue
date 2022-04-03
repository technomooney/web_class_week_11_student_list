<template>
  <tr v-bind:class="{present: student.present, absent: !student.present}">
    <td>{{student.name}}</td>
    <td>{{student.starID}}</td>
    <td>
      <input type="checkbox" v-bind:checked="student.present" @change="arrivedOrLeft(student,$event.target.checked)">
    </td>
    <td><img src="@/assets/delete-icon.png" height="20" @click="deleteStudent"></td>
  </tr>
</template>

<script>
export default {
  name: "StudentRow",
  props: {
    student:Object
  },
  methods: {
    arrivedOrLeft(student,present) {
      this.$emit("student-arrived-or-left-row",student, present)
    },
    deleteStudent() {
      this.$emit("delete-student-row", this.student)
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
</style>