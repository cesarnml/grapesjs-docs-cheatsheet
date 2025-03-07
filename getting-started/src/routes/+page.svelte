<div class="panel__top">
  <div class="panel__basic-actions"></div>
  <div class="panel__devices"></div>

  <div class="panel__switcher"></div>
</div>
<div class="editor-row">
  <div class="editor-canvas">
    <div id="gjs">
      <h1>Hello World Component!</h1>
    </div>
  </div>
  <div class="panel__right">
    <div class="layers-container"></div>
    <div class="styles-container"></div>
    <div class="traits-container"></div>
  </div>
</div>
<div id="blocks"></div>

<style lang="postcss">
  .panel__top {
    padding: 0;
    width: 100%;
    display: flex;
    position: initial;
    justify-content: center;
    justify-content: space-between;
  }

  .panel__basic-actions {
    position: initial;
  }

  .editor-row {
    display: flex;
    justify-content: flex-start;
    align-items: stretch;
    flex-wrap: nowrap;
    height: 300px;
  }

  .editor-canvas {
    flex-grow: 1;
  }

  .panel__right {
    flex-basis: 230px;
    position: relative;
    overflow-y: auto;
  }

  .panel__switcher {
    position: initial;
  }

  .panel__devices {
    position: initial;
  }
</style>
