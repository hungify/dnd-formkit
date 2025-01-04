<script setup lang="ts">
import { useDragAndDrop } from "@formkit/drag-and-drop/vue";
import { ref } from "vue";

const generateItems = (count: number, prefix: string) => {
  const items = [];
  for (let i = 0; i < count; i++) {
    items.push({
      id: i,
      name: `${prefix}-${i + 1}`,
    });
  }
  return items;
};

const items1 = ref(generateItems(40, "A"));
const items2 = ref(generateItems(40, "B"));
const items3 = ref(generateItems(40, "C"));
const items4 = ref(generateItems(40, "D"));

const showNote = ref(false);

// Configuration 1: nativeDrag is true
const [parent1, list1] = useDragAndDrop(items1.value, {
  nativeDrag: true,
});

// Configuration 2: nativeDrag = true and longPress = true
const [parent2, list2] = useDragAndDrop(items2.value, {
  nativeDrag: true,
  longPress: true,
  longPressDuration: 100,
});

// Configuration 3: nativeDrag = false
const [parent3, list3] = useDragAndDrop(items3.value, {
  nativeDrag: false,
});

// Configuration 4: nativeDrag = false and longPress = true
const [parent4, list4] = useDragAndDrop(items4.value, {
  nativeDrag: false,
  longPress: true,
  longPressDuration: 100,
});
</script>

<template>
  <div>
    <button @click="showNote = !showNote" class="toggle">
      {{ showNote ? 'Hide' : 'Show' }} Configurations
    </button>
    <p v-if="showNote">
      The configurations are as follows:
      <ul>
        <li><code>Config 1</code>: nativeDrag is true</li>
        <li><code>Config 2</code>: nativeDrag is true and longPress is true</li>
        <li><code>Config 3</code>: nativeDrag is false</li>
        <li><code>Config 4</code>: nativeDrag is false and longPress is true</li>
      </ul>
    </p>
    <div class="container">
      <div class="column">
        <h3><code>Config 1</code></h3>
        <ul ref="parent1" class="grid">
          <li
            v-for="item in list1"
            :key="item.id"
            class="grid-item"
            @contextmenu.prevent
          >
            <div>{{ item.name }}</div>
          </li>
        </ul>
      </div>

      <div class="column">
        <h3><code>Config 2</code></h3>
        <ul ref="parent2" class="grid">
          <li
            v-for="item in list2"
            :key="item.id"
            class="grid-item"
            @contextmenu.prevent
          >
            <div>{{ item.name }}</div>
          </li>
        </ul>
      </div>

      <div class="column">
        <h3><code>Config 3</code></h3>
        <ul ref="parent3" class="grid">
          <li
            v-for="item in list3"
            :key="item.id"
            class="grid-item"
            @contextmenu.prevent
          >
            <div>{{ item.name }}</div>
          </li>
        </ul>
      </div>

      <div class="column">
        <h3><code>Config 4</code></h3>
        <ul ref="parent4" class="grid">
          <li
            v-for="item in list4"
            :key="item.id"
            class="grid-item"
            @contextmenu.prevent
          >
            <div>{{ item.name }}</div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style>
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.3rem;
}

.column {
  border: 1px solid #4caf50;
  padding: 0 10px 10px;
}

.column h3 {
  text-align: center;
  margin: 4px 0;
}

.column:nth-child(1) .grid-item {
  background: #ff5722;
}

.column:nth-child(2) .grid-item {
  background: #2196f3;
}

.column:nth-child(3) .grid-item {
  background: #ffeb3b;
  color: black;
}

.column:nth-child(4) .grid-item {
  background: #9c27b0;
}

.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.5rem;
  padding: 0;
  width: 100%;
  justify-items: center;
  margin-top: 0;
}

.grid-item {
  color: white;
  text-align: center;
  width: 100%;
  height: 100px;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: transform 0.3s ease, opacity 0.3s ease;
  user-select: none;
  -webkit-user-select: none;
}

.placeholder {
  opacity: 0;
}

.dragging {
  transform: scale(1.1);
  opacity: 0.5;
}

.toggle {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 5px;
  margin-bottom: 10px;
  transition: background-color 0.3s ease;
}

.toggle:hover {
  background-color: #45a049;
}
</style>
