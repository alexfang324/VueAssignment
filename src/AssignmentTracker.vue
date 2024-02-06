<script>
import assignments from "./assets/assignments.json";

export default {
  //data to pass to template
  data() {
    return {
      assignments: assignments,
      hideCompleted: false,
    };
  },

  //dynamically computed variables
  computed: {
    filteredAssignment() {
      return this.hideCompleted
        ? this.assignments.filter((a) => a.percentComplete < 100)
        : this.assignments;
    },
  },
};
</script>

<template>
  <div class="container">
    <h1>Things on my plate</h1>
    <input type="checkbox" v-model="hideCompleted" /><label
      >hide finished assignments</label
    >
    <div
      v-for="(assignment, index) in filteredAssignment"
      :key="assignment.title"
      class="assignment-card"
    >
      <h3>{{ index + 1 }}: {{ assignment.title }}</h3>
      <p>Due Date: {{ assignment.dueDate }}</p>
      <p>
        Days Remaining:
        {{
          Math.ceil(
            (Date.parse(assignment.dueDate) - Date.now()) / (1000 * 3600 * 24)
          )
        }}
      </p>
      <p>Percent Completed: {{ assignment.percentComplete }}%</p>
    </div>
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  font-size: 36px;
  margin-bottom: 20px;
}

input[type="checkbox"] {
  width: 25px;
  height: 25px;
  margin-bottom: 10px;
}
label {
  font-size: 30px;
}

.assignment-card {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.assignment-card h3 {
  font-size: 24px;
  margin-bottom: 10px;
}

.assignment-card p {
  margin-bottom: 8px;
}
</style>
