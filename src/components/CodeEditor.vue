<script setup lang="ts">
import { ref, type Ref } from "vue";
import CodeMirror from "vue-codemirror6";

import { javascript, esLint } from "@codemirror/lang-javascript";
import { linter, lintGutter } from "@codemirror/lint";
import { oneDark } from "@codemirror/theme-one-dark";
import type { Extension } from "@codemirror/state";
// @ts-ignore
import * as eslint from "eslint-linter-browserify";

const cm: Ref<InstanceType<typeof CodeMirror> | undefined> = ref();
const value: Ref<string> = ref(`console.log('caca')`);

  const config : any = {
  parserOptions: {
    ecmaVersion: 2022,
    sourceType: "module",
  },
  env: {
    browser: true,
    node: true,
  },
};


const extensions: Extension[] = [
  lintGutter(),
  linter(esLint(new eslint.Linter(), config)),
  oneDark,
];
</script>

<template>
  <CodeMirror
    ref="cm"
    v-model="value"
    :lang="javascript()"
    :dark="true"
    :extensions="extensions"
    class="min-h-screen"
    gutter
    basic
    wrap
  />
</template>

<style>
.cm-editor {
  height: 100vh !important;
}
</style>
