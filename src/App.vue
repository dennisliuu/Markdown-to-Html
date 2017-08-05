<template>
  <div id="app">
    <div class="ts large header">
      <i class="announcement top aligned icon"></i>
      <div class="content">
        <a href="https://wastemobile.gitbooks.io/gitbook-chinese/content/format/markdown.html" target="__blank" class="unstyled">Markdown</a> to Html
        <div class="sub header"><!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/dennisliuu/Markdown-to-Html" data-icon="octicon-star" aria-label="Star dennisliuu/Markdown-to-Html on GitHub">Star</a></div>
      </div>
    </div>
    <div class="container">
      <div class="one fade-in-right">
        <div class="ts fluid focus input massive">
          <textarea id="md-area" placeholder="Markdown" v-model="input"></textarea>
        </div>
        <div class="ts fluid bottom attached buttons">
          <button class="ts ts negative basic button" @click="decreasebutton">
            <i class="minus left icon"></i>minus
          </button>
          <button class="ts positive basic button" @click="increasebutton">
            <i class="plus left icon"></i> PLUS
          </button>
          <button class="ts primary basic button" @click="resetboth">
            <i class="undo icon"></i> Reset
          </button>
        </div>
      </div>
  
      <div class="two fade-in-left raw-html">
        <div class="ts fluid input massive" style="font-size: 16px">
          <div v-if="viewmd">
            <pre><code v-html="rawHtml" id="html-area"></code></pre>
          </div>
          <div v-if="!viewmd">
            <pre><code v-html="viewHtml" id="html-area"></code></pre>
          </div>
        </div>
        <div class="ts fluid bottom attached buttons">
          <button class="ts negative basic button" @click="showmd">
            <i class="code icon"></i> {{ currentview }}
          </button>
          <button class="ts primary basic button copyevent" @click="copyhtml">
            <i class="copy icon"></i> COPY
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import highlight from '@/utils/highlight'
import marked3 from 'marked3'

export default {
  data() {
    return {
      input: '',
      viewmd: true,
      currentview: 'Html'
    }
  },
  computed: {
    rawHtml() {
      return highlight(marked3(this.input))
    },
    viewHtml() {
      return marked3(this.input)
    }
  },
  methods: {
    increasebutton() {
      var el_md = document.getElementById('md-area')
      var el_html = document.getElementById('html-area')
      var style = window.getComputedStyle(el_md, null).getPropertyValue('font-size')
      var fontSize = parseFloat(style);

      el_md.style.fontSize = (fontSize + 2) + 'px'
      el_html.style.fontSize = (fontSize + 2) + 'px'
    },
    decreasebutton() {
      var el_md = document.getElementById('md-area')
      var el_html = document.getElementById('html-area')
      var style = window.getComputedStyle(el_md, null).getPropertyValue('font-size')
      var fontSize = parseFloat(style);

      el_md.style.fontSize = (fontSize - 2) + 'px'
      el_html.style.fontSize = (fontSize - 2) + 'px'
    },
    resetboth() {
      document.getElementById('md-area').value = "";
      document.getElementById('html-area').innerText = "";
      document.getElementById('md-area').style.fontSize = '16px'
      document.getElementById('html-area').style.fontSize = '16px'
    },
    showmd() {
      if (this.currentview === 'View') {
        this.currentview = 'Html'
      }
      else
        this.currentview = 'View'
      this.viewmd = !this.viewmd
    },
    copyhtml() {
      var copyarea = document.querySelector('#html-area')
      var range = document.createRange();
      range.selectNode(copyarea);
      window.getSelection().addRange(range);
      document.execCommand("copy");
    }
  }
}
</script>

<style src="highlight.js/styles/github.css"></style>
<style>
* {
  box-sizing: border-box;
}

a {
  color: green;
}

html,
body,
#app {
  height: 100%;
  overflow-y: hidden;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  /* margin-top: 60px; */
  font-size: 12px;
  text-align: left;
  padding: 30px;
  height: 100%;
  min-width: 470px;
  line-height: 2em;
}

textarea {
  font-size: 16px;
}

.massive {
  height: 80vh;
  padding: 0;
  margin: 0;
}

.raw-html {
  width: 50%;
  height: 100%;
  background-color: #f9f9f9;
}

.raw-html pre {
  height: 100%;
  margin: 0;
  padding: 20px;
  overflow: auto;
  white-space: pre-wrap;
  word-break: break-word;
}

.container>div {
  float: left;
  width: 45%;
  margin-right: 10%;
  padding: 2%;
  background: #fff;
  position: relative;
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.2);
}

.container>.two {
  margin-right: 0;
}

.fade-in-left {
  animation: animateLeft 2s;
  -moz-animation: animateLeft 2s;
  /* Firefox */
  -webkit-animation: animateLeft 1s;
  /* Safari and Chrome */
  -o-animation: animateLeft 2s;
  /* Opera */
}

.fade-in-right {
  animation: animateRight 1s;
  -moz-animation: animateRight 1s;
  /* Firefox */
  -webkit-animation: animateRight 1s;
  /* Safari and Chrome */
  -o-animation: animateRight 1s;
  /* Opera */
}





















/* ANIMATE LEFT */

@keyframes animateLeft {
  from {
    opacity: 0;
    left: -100px;
  }
  to {
    opacity: 1;
    left: 0;
  }
}

@-moz-keyframes animateLeft {
  /* Firefox */
  from {
    opacity: 0;
    right: -100px;
  }
  to {
    opacity: 1;
    right: 0;
  }
}

@-webkit-keyframes animateLeft {
  /* Safari and Chrome */
  from {
    opacity: 0;
    right: -100px;
  }
  to {
    opacity: 1;
    right: 0;
  }
}

@-o-keyframes aninateLeft {
  /* Opera */
  from {
    opacity: 0;
    right: -100px;
  }
  to {
    opacity: 1;
    right: 0;
  }
}




















/* ANIMATE RIGHT */

@keyframes animateRight {
  from {
    opacity: 0;
    left: -100px;
  }
  to {
    opacity: 1;
    left: 0;
  }
}

@-moz-keyframes animateRight {
  /* Firefox */
  from {
    opacity: 0;
    left: -100px;
  }
  to {
    opacity: 1;
    left: 0;
  }
}

@-webkit-keyframes animateRight {
  /* Safari and Chrome */
  from {
    opacity: 0;
    left: -100px;
  }
  to {
    opacity: 1;
    left: 0;
  }
}

@-o-keyframes aninateRight {
  /* Opera */
  from {
    opacity: 0;
    left: -100px;
  }
  to {
    opacity: 1;
    left: 0;
  }
}
</style>
