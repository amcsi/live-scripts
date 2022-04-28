<template>
  <span>
    <input
      :placeholder="label"
      :title="label"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      v-bind="$attrs"
    />
  </span>
</template>

<script>
/** @class InputWithLabel */
export default {
  name: 'InputWithLabel',
  data() {
    return {
      localValue: this.modelValue,
    };
  },
  props: {
    modelValue: String,
    label: String,
  },
  emits: ['update:modelValue']
};
</script>

<style scoped lang="scss">

</style>
