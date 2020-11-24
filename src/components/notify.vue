<template>
  <div class="notify">
    <template v-if="show">
      <BAlert :variant="notify" show>{{ notifyMsg }}</BAlert>
    </template>
  </div>
</template>

<script>
export default {
  name: "notify",
  props: {
    notify: {
      type: String,
      default: ""
    }
  },
  computed: {
    show() {
      return this.notify ? !!this.notify.length : false;
    },
    notifyMsg() {
      return this.notify === "success"
        ? "Verification passed successfully"
        : "Check failed";
    }
  }
};
</script>

<style lang="scss" scoped>
.notify {
  padding: 0.25rem 0;
}
</style>
