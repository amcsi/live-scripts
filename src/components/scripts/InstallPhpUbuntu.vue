<template>
  <div>
    <div>Installs a PHP version with extensions on Ubuntu using the <a
      target="_blank"
      href="https://launchpad.net/~ondrej/+archive/ubuntu/php"
    >Ondrej PPA</a>.
    </div>

    <InputWithLabel label="PHP version" v-model="phpVersion" />

    <div>
      <SourceCode :code="command" />
    </div>
  </div>
</template>

<script>
import SourceCode from '../SourceCode.vue';
import InputWithLabel from '../ui/InputWithLabel.vue';

/** @class InstallPhpUbuntu */
export default {
  name: 'InstallPhpUbuntu',
  components: { SourceCode, InputWithLabel },
  data() {
    return {
      phpVersion: '8.1',
      extensions: [
        'curl',
        'dev',
        'fpm',
        'gd',
        'mbstring',
        'pdo',
        'pdo-mysql',
        'pgsql',
        'redis',
        'simplexml',
        'soap',
        'sqlite3',
        'xdebug',
        'zip',
      ],
    }
  },
  computed: {
    command() {
      return `sudo apt install php${this.phpVersion} php${this.phpVersion}-{${this.extensions.join(',')}}`;
    }
  }
};
</script>

<style scoped lang="scss">

</style>
