<script setup lang="ts">
import { useRouter } from 'vue-router'
import { NButton, NSpace, NA } from 'naive-ui'
import BetaSearch from '../components/BetaSearch.vue'
import BetaCollapse from '../components/BetaCollapse.vue'
import categories from '../categories'

const router = useRouter()

const examples: string[] = []
for (const category of categories) {
  for (const subCategory of category.subCategories) {
    for (const example of subCategory.examples) {
      examples.push(example.expression)
    }
  }
}

function randomExample () {
  const example = examples[Math.floor(Math.random() * examples.length)]
  router.push({ name: 'Python', params: { expr: example } })
}
</script>

<template>
  <beta-search />
  <div
    style="width: calc(100vw - 24px);
  max-width: 600px;
  margin: auto;"
  >
    <h2
      style="
  text-align: center;
  font-size: 1.25em;
  font-weight: normal;
"
    >
      Examples
    </h2>
    <n-space vertical>
      <n-button
        secondary
        type="primary"
        @click="randomExample"
      >
        Random Example
      </n-button>
      <beta-collapse
        v-for="category in categories"
        :category="category"
      />
    </n-space>
    <p>
      … and more: see
      the
      <n-a
        href="https://docs.sympy.org"
        target="_blank"
      >
        documentation
      </n-a> to learn
      about the full range of SymPy's capabilities.
    </p>
  </div>
</template>
