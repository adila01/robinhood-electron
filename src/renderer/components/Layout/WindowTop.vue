<template>
<div class='window-top text-right' style="-webkit-app-region: drag">
  <div id="window-top-btns">
    <span @click="minimize" class="glyphicon glyphicon-chevron-down window-top-btn"></span>
    <span @click="maximize" class="glyphicon glyphicon-new-window window-top-btn"></span>
    <span @click="close" class="glyphicon glyphicon-remove window-top-btn"></span>
  </div>
</div>
</template>
<script>
const remote = require('electron').remote;

export default {
  created() {
    const window = remote.getCurrentWindow();

    window.on('resize', () => {
      this.adjustSize();
    });
  },
  mounted() {
    this.adjustSize();
  },
  methods: {
    adjustSize() {
      const window = remote.getCurrentWindow();
      const size = window.getSize();
      $('#content').css('height', `${size[1] - 75}px`);
    },
    minimize() {
      const window = remote.getCurrentWindow();
      window.minimize();
    },
    maximize() {
      const window = remote.getCurrentWindow();
      if (!window.isMaximized()) {
        window.maximize();
      } else {
        window.unmaximize();
      }
    },
    close() {
      const window = remote.getCurrentWindow();
      window.close();
    }
  }
};
</script>
