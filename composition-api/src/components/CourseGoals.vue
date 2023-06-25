<template>
  <div>
    <goals-list :goals="filteredGoals"></goals-list>
    <add-goal @add-goal="addGoal"></add-goal>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import GoalsList from "./GoalsList.vue";
import AddGoal from "./AddGoal.vue";

export default {
  components: {
    GoalsList,
    AddGoal,
  },
  setup() {
    const goals = ref([]);  // ref will create a wrapper object around []. when we change the array inside object, then Vue will know
    
    const filteredGoals = computed(() => {
      return goals.value.filter(
        (goal) => !goal.text.includes("Angular") && !goal.text.includes("React")
      );
    });
    
    function addGoals(text) {
      const newGoal = {
        id: new Date().toISOString(),
        text: text,
      };
      goals.value.push(newGoal);
    }
    
    return {
      // userGoals: goals  // name can be changed or not
      filteredGoals,
      addGoals
    };
  }
  // data() {
  //   return {
  //     goals: [],
  //   };
  // },
  // computed: {
  //   filteredGoals() {
  //     return this.goals.filter(
  //       (goal) => !goal.text.includes("Angular") && !goal.text.includes("React")
  //     );
  //   },
  // },
  // methods: {
  //   addGoal(text) {
  //     const newGoal = {
  //       id: new Date().toISOString(),
  //       text: text,
  //     };
  //     this.goals.push(newGoal);
  //   },
  // },
};
</script>