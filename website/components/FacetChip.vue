<template>
  <div
    class="px-4 py-2 mr-2 border border-gray-900 rounded-lg hover:bg-gray-900 hover:text-white cursor-pointer transition-default"
    style="width: max-content;"
    :class="[active ? 'bg-gray-900 text-white' : '']"
    @click="emitClicked"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ["active"],

  methods: {
    emitClicked() {
      this.$emit("clicked");
    }
  }
};
</script>
