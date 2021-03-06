<template>
  <div id="app">

    <header>
      <h1>v-tooltip</h1>
      <div class="command">npm install --save v-tooltip</div>
      <nav>
        <a href="https://github.com/Akryum/vue-tooltip"><img src="https://img.shields.io/github/stars/Akryum/vue-tooltip.svg?style=social&label=Star" /></a>
        <a href="https://www.npmjs.com/package/v-tooltip">
          <img src="https://img.shields.io/npm/v/v-tooltip.svg" />
          <img src="https://img.shields.io/npm/dm/v-tooltip.svg" />
        </a>
        <a href="https://vuejs.org/"><img src="https://img.shields.io/badge/vue-2.0-orange.svg" /></a>
      </nav>
    </header>

    <section class="demo">
      <div class="section-content">
        <h2>Reactive content</h2>
        <input class="tooltip-content" v-model="msg" placeholder="Tooltip content" />

        <button class="tooltip-target" v-tooltip.top-center="msg">Hover me</button>
      </div>
    </section>

    <section class="snippets">
      <Collapse title="Show code">
        <div class="section-content">
          <CodeSnippet class="snippet" :code="mainSnippet" lang="js"/>
          <div class="plus">+</div>
          <CodeSnippet class="snippet" :code="componentSnippet1" lang="html"/>
          <div class="plus">+</div>
          <CodeSnippet class="snippet" :code="styleSnippet1" lang="scss"/>
        </div>
      </Collapse>
    </section>

    <section class="demo">
      <div class="section-content">
        <h2>With dynamic classes</h2>
        <button class="tooltip-target" v-tooltip="{ content: msg, position: 'top-center', classes: ['danger'] }">Hover me</button>
      </div>
    </section>

    <section class="snippets">
      <Collapse title="Show code">
        <div class="section-content">
          <CodeSnippet class="snippet" :code="componentSnippet2" lang="html"/>
          <div class="plus">+</div>
          <CodeSnippet class="snippet" :code="styleSnippet2" lang="scss"/>
        </div>
      </Collapse>
    </section>

    <section class="more">
      <div class="section-content">
        And much <a href="https://github.com/Akryum/v-tooltip#usage">More</a>!
      </div>
    </section>

  </div>
</template>

<script>
import CodeSnippet from './CodeSnippet.vue'
import Collapse from './Collapse.vue'

const mainSnippet = `
import Vue from 'vue'
import VTooltip from 'v-tooltip'

Vue.use(VTooltip)

new Vue({
  data: {
    msg: 'This is a button.'
  }
})
`

const componentSnippet1 = `
<button v-tooltip.top-center="msg">Hover me</button>
`

const styleSnippet1 = `
.tooltip {
  display: block !important;
  z-index: 10000;

  .tooltip-inner {
    background: black;
    color: white;
    border-radius: 16px;
    padding: 5px 10px 4px;
  }

  .tooltip-arrow {
    width: 0;
    height: 0;
    border-style: solid;
    position: absolute;
    margin: 5px;
    border-color: black;
  }
  
  &[x-placement^="top"] {
    margin-bottom: 5px;
    
    .tooltip-arrow {
      border-width: 5px 5px 0 5px;
      border-left-color: transparent !important;
      border-right-color: transparent !important;
      border-bottom-color: transparent !important;
      bottom: -5px;
      left: calc(50% - 5px);
      margin-top: 0;
      margin-bottom: 0;
    }
  }
  
  &[x-placement^="bottom"] {
    margin-top: 5px;
    
    .tooltip-arrow {
      border-width: 0 5px 5px 5px;
      border-left-color: transparent !important;
      border-right-color: transparent !important;
      border-top-color: transparent !important;
      top: -5px;
      left: calc(50% - 5px);
      margin-top: 0;
      margin-bottom: 0;
    }
  }
  
  &[x-placement^="right"] {
    margin-left: 5px;

    .tooltip-arrow {
      border-width: 5px 5px 5px 0;
      border-left-color: transparent !important;
      border-top-color: transparent !important;
      border-bottom-color: transparent !important;
      left: -5px;
      top: calc(50% - 5px);
      margin-left: 0;
      margin-right: 0;
    }
  }

  &[x-placement^="left"] {
    margin-right: 5px;

    .tooltip-arrow {
      border-width: 5px 0 5px 5px;
      border-top-color: transparent !important;
      border-right-color: transparent !important;
      border-bottom-color: transparent !important;
      right: -5px;
      top: calc(50% - 5px);
      margin-left: 0;
      margin-right: 0;
    }
  }

  &[aria-hidden='true'] {
    visibility: hidden;
    opacity: 0;
    transition: opacity .15s, visibility .15s;
  }

  &[aria-hidden='false'] {
    visibility: visible;
    opacity: 1;
    transition: opacity .15s;
  }
}
`

const componentSnippet2 = `
<button v-tooltip="{
  content: msg,
  position: 'top-center',
  classes: ['danger'],
}">Hover me</button>`

const styleSnippet2 = `
.tooltip {
  &.danger {
    .tooltip-inner {
      background: #ee8888;
      color: black;
    }

    .tooltip-arrow {
      border-color: #ee8888;
    }
  }
}
`

export default {
  name: 'app',
  components: {
    CodeSnippet,
    Collapse,
  },
  data () {
    return {
      msg: `This is a button.`,
      mainSnippet,
      componentSnippet1,
      styleSnippet1,
      componentSnippet2,
      styleSnippet2,
    }
  },
}
</script>

<style lang="scss">
@import "~style/imports";

body {
  margin: 0;
  background: #fcfcfc;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

header {
  background: $primary-color;
  padding: 64px 32px;

  nav {
    text-align: center;
  }
}

section {
  .section-content {
    max-width: 560px;
    margin: auto;
    padding: 64px 0;
    box-sizing: border-box;
  }
}

.collapse {
  .section-content {
    padding: 12px 0 64px 0;
  }
}

h1 {
  color: white;
  font-weight: normal;
  text-align: center;
  margin: 0 0 32px;
}

h2 {
  &:first-child {
    margin-top: 0;
  }

  font-weight: normal;
}

a {
  color: $primary-color;
  text-decoration: none;
  cursor: pointer;

  &:hover {
    color: lighten($primary-color, 10%);
  }
}

button,
input {
  font-size: inherit;
  font-family: inherit;
  border: none;
  outline: none;
  padding: 12px 24px;
  border-radius: 2px;
}

button {
  color: $md-grey;
  background: white;
  border: solid 2px $md-grey;
  cursor: pointer;
  display: inline-block;
  text-align: center;
  transition: background .3s;

  &:hover {
    background: lighten($md-grey, 30%);
  }
}

input {
  background: white;
  display: block;
  margin-bottom: 12px;
  width: 100%;
  box-sizing: border-box;
  border-bottom: solid 2px $md-grey-300;
  border-right: solid 1px $md-grey-100;
  text-align: left;

  &:focus {
    border-bottom-color: $primary-color;
  }
}

.tooltip {
  display: block !important;
  z-index: 10000;

  .tooltip-inner {
    background: black;
    color: white;
    border-radius: 16px;
    padding: 5px 10px 4px;
  }

  .tooltip-arrow {
    width: 0;
    height: 0;
    border-style: solid;
    position: absolute;
    margin: 5px;
    border-color: black;
  }
  
  &[x-placement^="top"] {
    margin-bottom: 5px;
    
    .tooltip-arrow {
      border-width: 5px 5px 0 5px;
      border-left-color: transparent !important;
      border-right-color: transparent !important;
      border-bottom-color: transparent !important;
      bottom: -5px;
      left: calc(50% - 5px);
      margin-top: 0;
      margin-bottom: 0;
    }
  }
  
  &[x-placement^="bottom"] {
    margin-top: 5px;
    
    .tooltip-arrow {
      border-width: 0 5px 5px 5px;
      border-left-color: transparent !important;
      border-right-color: transparent !important;
      border-top-color: transparent !important;
      top: -5px;
      left: calc(50% - 5px);
      margin-top: 0;
      margin-bottom: 0;
    }
  }
  
  &[x-placement^="right"] {
    margin-left: 5px;

    .tooltip-arrow {
      border-width: 5px 5px 5px 0;
      border-left-color: transparent !important;
      border-top-color: transparent !important;
      border-bottom-color: transparent !important;
      left: -5px;
      top: calc(50% - 5px);
      margin-left: 0;
      margin-right: 0;
    }
  }

  &[x-placement^="left"] {
    margin-right: 5px;

    .tooltip-arrow {
      border-width: 5px 0 5px 5px;
      border-top-color: transparent !important;
      border-right-color: transparent !important;
      border-bottom-color: transparent !important;
      right: -5px;
      top: calc(50% - 5px);
      margin-left: 0;
      margin-right: 0;
    }
  }

  &[aria-hidden='true'] {
    visibility: hidden;
    opacity: 0;
    transition: opacity .15s, visibility .15s;
  }

  &[aria-hidden='false'] {
    visibility: visible;
    opacity: 1;
    transition: opacity .15s;
  }

  &.danger {
    .tooltip-inner {
      background: #ee8888;
      color: black;
    }

    .tooltip-arrow {
      border-color: #ee8888;
    }
  }
}

.command {
  background: darken($primary-color, 10%);
  color: white;
  font-family: monospace;
  max-width: 500px;
  margin: 12px auto;
  border-radius: 2px;
  padding: 12px 24px;
  box-sizing: border-box;
}

.snippet {
  margin: 16px 0;
}

.plus {
  text-align: center;
  color: $primary-color;
  font-size: 32px;
  margin: 12px;
}

.snippets {

}

.demo {
  background: #eee;

  .section-content {
    text-align: center;
  }

  button {
    margin-top: 24px;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    padding: 0;
    text-transform: uppercase;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 16px;
    transform: rotate(-12deg);
  }
}

.more {
  font-size: 24px;
  text-align: center;
  background: lighten($primary-color, 45%);
}

</style>
