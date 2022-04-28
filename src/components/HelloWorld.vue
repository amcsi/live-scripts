<script setup lang="ts">
import { computed, ref } from 'vue';
import SourceCode from './SourceCode.vue';
import InstallPhpUbuntu from './scripts/InstallPhpUbuntu.vue';

defineProps<{ msg: string }>()

const count = ref(0)

const sourcePhpVersion = ref('8.0');
const targetPhpVersion = ref('8.1');
const modIniFiles = ref('sqlsrv.ini pdo_sqlsrv.ini');
const symlinkedIniFiles = ref('30-pdo_sqlsrv.ini');

const code = computed(() => {
  const modIniFilesToCopy = modIniFiles.value.split(/\s+/).map(filename => `mods-available/${filename}`).join(' ');
  const symlinkedIniFilesToCopy = symlinkedIniFiles.value.split(/\s+/).map(filename => `fpm/conf.d/${filename} cli/conf.d/${filename}`).join(' ');

  return `cd /etc/${sourcePhpVersion.value}
  cp --no-dereference --parents ${modIniFilesToCopy} ${symlinkedIniFilesToCopy} ../${targetPhpVersion.value}/
  `
})
</script>

<template>
  <div>
    <div class="container">
      Copies PHP config files over to new PHP version directory in Ubuntu:

      <div>
        <input type="text" title="Source PHP version" placeholder="Source PHP version" v-model="sourcePhpVersion" />
        <input type="text" title="Target PHP version" placeholder="Target PHP version" v-model="targetPhpVersion" />
        <input type="text" title="Base ini files" placeholder="Base ini files" v-model="modIniFiles" />
        <input type="text" title="Symlinked ini files" placeholder="Symlinked ini files" v-model="symlinkedIniFiles" />
      </div>
      <SourceCode :code="code" />
    </div>

    <InstallPhpUbuntu />
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}

.container {
  text-align: left;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
