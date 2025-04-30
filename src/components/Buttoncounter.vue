<template>
  <div>
    <button @click="incrementCounter">{{ buttonLabel }} : {{ count }}</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  props: {
    buttonLabel: {
      type: String,
      required: true,
      default: "Click Me",
    },
  },
  methods: {
    incrementCounter() {
      this.count++;
    },
  },
};
</script>
