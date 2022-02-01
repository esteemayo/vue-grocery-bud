<template>
  <p :class="`alert alert-${alert.type}`">{{ alert.msg }}</p>
</template>

<script>
export default {
  name: 'Alert',
  props: {
    alert: Object,
    hideAlert: Function,
  },
  mounted() {
    const timeout = setTimeout(() => {
      this.hideAlert();
    }, 3000);

    return () => clearInterval(timeout);
  },
};
</script>

<style></style>
