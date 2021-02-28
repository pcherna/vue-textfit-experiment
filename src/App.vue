<template>
  <div v-cloak id="app">

    <div>
      <div class="fixed-text-ok">
        1: (OK) div is unconditionally shown (single-line example)
      </div>
      <div >
        <TextFit class="fitted-text"  :minFontSize="10" :maxFontSize="200">Here is some sample text that we want to automatically adjust to fit inside our bounding box.</TextFit>
      </div>
    </div>

    <div>
      <div class="fixed-text-ok">
        2: (OK) div is unconditionally shown (multi-line example)
      </div>
      <div>
        <TextFit class="fitted-text" multiLine :minFontSize="10" :maxFontSize="200">Here is some sample text that we want to automatically adjust to fit inside our bounding box.</TextFit>
      </div>
    </div>

    <div v-show="ready">
      <div class="fixed-text-bad">
        3: (Broken) div with delayed v-show
      </div>
      <div>
        <TextFit class="fitted-text" multiLine :minFontSize="10" :maxFontSize="200">Here is some sample text that we want to automatically adjust to fit inside our bounding box.</TextFit>
      </div>
    </div>

    <div v-show="ready">
      <div class="fixed-text-ok">
        4: (OK) div has delayed v-show but requires explicit v-show on &lt;TextFit&gt; component
      </div>
      <div>
        <TextFit v-show="ready" class="fitted-text" multiLine :minFontSize="10" :maxFontSize="200">Here is some sample text that we want to automatically adjust to fit inside our bounding box.</TextFit>
      </div>
    </div>

    <div v-show="ready">
      <div class="fixed-text-bad">
        5: (Broken) div with delayed v-show, even with explicit dims to &lt;TextFit&gt; 
      </div>
      <div>
        <TextFit class="fitted-text" :width="1024" :height="200" multiLine :minFontSize="10" :maxFontSize="200">Here is some sample text that we want to automatically adjust to fit inside our bounding box.</TextFit>
      </div>
    </div>

  </div>
</template>

<script>
import TextFit from './components/TextFit.vue'

export default {
  name: 'App',
  components: {
    TextFit,
  },
  data () {
    return {
      ready: false,
    }},
  mounted() {
    // Just a simple delay on when we show the div
    setTimeout(() => this.ready = true, 1000)
  }
}
</script>

<style>
/* Initially-hide everything inside an element with attr:v-cloak */
[v-cloak]>* {
    display: none;
}

.fixed-text-ok, .fixed-text-bad {
  font-family: "Arial";
  font-size: 30px;
  width: 1004px;
  margin-top: 50px;
  margin-bottom: 10px;
  padding: 10px;
}
.fixed-text-ok {
  background-color: lightgreen;
}

.fixed-text-bad {
  background-color: lightcoral;
}

.fitted-text {
  font-family: "Arial";
  background-color: lightblue;
  width: 1024px;
  height: 200px
}
</style>
