<script setup>
import { ref, computed } from 'vue'

const x = ref(0)
const y = ref(0)

// 用普通物件包住 ref：
// 模板中 refs.x 是「嵌套屬性」，不會被自動解包，能拿到 ref 本身
const refs = { x, y }

const z = computed(() => x.value + y.value)

function increment(target) {
  target.value++
}

function decrement(target) {
  if (target.value > 0) target.value--
}
</script>

<template>
  <div class="calculator">
    <h1>小計算機</h1>

    <div class="row">
      <!-- x -->
      <div class="operand">
        <span class="label">x</span>
        <p class="number">{{ x }}</p>
        <div class="controls">
          <button class="minus" @click="decrement(refs.x)">−</button>
          <button class="plus" @click="increment(refs.x)">+</button>
        </div>
      </div>

      <span class="operator">+</span>

      <!-- y -->
      <div class="operand">
        <span class="label">y</span>
        <p class="number">{{ y }}</p>
        <div class="controls">
          <button class="minus" @click="decrement(refs.y)">−</button>
          <button class="plus" @click="increment(refs.y)">+</button>
        </div>
      </div>

      <span class="operator">=</span>

      <!-- z -->
      <div class="operand result">
        <span class="label">z</span>
        <p class="number">{{ z }}</p>
        <div class="controls placeholder"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  font-family: system-ui, sans-serif;
  background: #f7f9f8;
  padding: 2rem;
  box-sizing: border-box;
}

h1 {
  color: #333;
  margin-bottom: 3rem;
  font-size: 2rem;
}

.row {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.25rem;
}

.operand {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 160px;
  height: 220px;
  padding: 1.25rem 1rem;
  box-sizing: border-box;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
}

.result {
  background: #eaf7f1;
}

.label {
  font-size: 1rem;
  font-weight: bold;
  color: #888;
}

.number {
  font-size: 3.5rem;
  font-weight: bold;
  color: #42b883;
  margin: 0;
  line-height: 1;
  font-variant-numeric: tabular-nums;
}

.controls {
  display: flex;
  gap: 0.6rem;
}

.operator {
  width: 40px;
  text-align: center;
  font-size: 2.5rem;
  font-weight: bold;
  color: #666;
  flex-shrink: 0;
}

button {
  width: 48px;
  height: 48px;
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.2s, transform 0.1s;
}

.plus {
  background: #42b883;
}

.plus:hover {
  background: #369e6e;
}

.minus {
  background: #ff8b8b;
}

.minus:hover {
  background: #e96f6f;
}

button:active {
  transform: scale(0.94);
}

@media (max-width: 720px) {
  .row {
    flex-direction: column;
    gap: 0.75rem;
  }

  .operand {
    width: 200px;
    height: auto;
    gap: 0.75rem;
  }

  .operator {
    width: auto;
    font-size: 1.8rem;
  }

  .placeholder {
    display: none;
  }
}
</style>