
<template>
  <div class="my-element">
    <p v-on:click="scannerReady()" :style="textStyle">I am a custom element !</p>
  </div>
  <card-reader
    @ready="scannerReady"
    @error="scannerError"
    @uid="handleUid"
    @info="handleInfo"
  />
  <p>STATUS: {{ status }}</p>
  <p>UID: {{ uid }}</p>
  <p>INFO: {{ info }}</p>
</template>

<script>
import NFCRead from '@helios-interactive/vue-nfc-reader';
Vue.use(NFCRead, { host: 'http://localhost', port: 3333 });
export default {
  props: {
    content: { type: Object, required: true },
  },
  computed: {
    textStyle() {
      return {
        color: this.content.textColor,
      };
    },
  },
  data() {
    return {
      status: '[scanner status]',
      uid: '',
      info: '',
    };
  },
  methods: {
    scannerReady() {
      this.status = 'Ready to scan';
    },
    scannerError(error) {
      this.status = `Error: ${error.message}`;
    },
    handleUid(uid) {
      this.uid = uid;
    },
    handleInfo(data) {
      this.info = data;
    },
  },
};
</script>

<style lang="scss" scoped>
.my-element {
  p {
    font-size: 18px;
  }
}
</style>
