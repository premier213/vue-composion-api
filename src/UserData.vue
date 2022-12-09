<template>
  <div>
    {{ uName }}
  </div>
</template>

<script lang="ts">
import {
  computed,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from "vue";

export default {
  props: ["username", "age"],
  setup(props, ctx) {
    const uName = computed(() => {
      return (
        "My name is " + props.username + " and " + props.age + " Years old."
      );
    });
    onBeforeMount(() => console.log("onBeforeMount"));
    onMounted(() => console.log("onMounted"));
    onBeforeUpdate(() => console.log("onBeforeUpdate"));
    onUpdated(() => console.log("onUpdated"));
    onBeforeUnmount(() => console.log("onBeforeUnmount"));
    onUnmounted(() => console.log("onUnmounted"));

    return { uName };
  },
};
</script>
