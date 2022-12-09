<template>
  <div>fullname : {{ fullname }}</div>
  <div>firstname: {{ user.name }}</div>
  <div>lastname: {{ user.family }}</div>
  <div>age: {{ user.age }}</div>
  <div>job: {{ job.vocation }}</div>
  <div>specialty: {{ job.framework }}</div>
  <div>references: {{ reference }}</div>
  <div>react: {{ react }}</div>
  <div>to reference: {{ toReference }}</div>
  <div>car: {{ car }}</div>
  <input type="text" placeholder="name" @input="setFirstname" /><br />
  <input type="text" placeholder="family" ref="lastNameInput" /><br />
  <input type="text" placeholder="select car" v-model="car" /><br />
  <button @click="setFramework">Set New Framework</button><br />
  <button @click="setNewAge">Set New age</button><br />
  <button @click="setLastname">setLastname</button><br />
  ---------- <br />
  <UserData :username="user.name" :age="user.age" />
</template>

<script lang="ts">
import { ref, reactive, isRef, isReactive, toRefs, computed, watch } from "vue";
import UserData from "./UserData.vue";

export default {
  components: {
    UserData,
  },
  setup() {
    const user = ref({
      name: "",
      family: "",
      age: 31,
    });

    const job = reactive({
      vocation: "programmer",
      framework: "vue",
    });

    const car = ref("");
    const lastNameInput = ref(null);

    const reference = isRef(user);
    const react = isReactive(job);
    const toReference = toRefs(user.value);

    setTimeout(() => {
      (user.value.name = "ali"), (user.value.age = 30);
    }, 2000);

    watch([car, user.value], (oldStates, newStates) => {
      console.log("car", oldStates[0], "newCar", newStates[0]);
      console.log("user", oldStates[1], "newUser", newStates[1]);
    });

    function setFramework() {
      job.framework = "react";
    }

    function setNewAge() {
      user.value.age = 40;
    }

    function setFirstname(event: Event) {
      user.value.name = event?.target?.value;
    }

    function setLastname() {
      user.value.family = lastNameInput.value.value;
    }

    const fullname = computed(() => user.value.name + " " + user.value.family);

    return {
      user,
      job,
      reference,
      react,
      toReference,
      setFramework,
      setNewAge,
      setFirstname,
      setLastname,
      fullname,
      car,
      lastNameInput,
    };
  },
};
</script>
