<template>
  <div>
    <pre>{{ formattedCode }}</pre>
  </div>
</template>

<script>
/** @class SourceCode */
export default {
  name: 'SourceCode',
  props: {
    code: String,
    default: '',
  },
  computed: {
    formattedCode() {
      return this.code.split('\n').map(line => line.trim()).join('\n');
    },
  }
};
</script>

<style scoped lang="scss">

</style>
