<script setup lang="ts">
import { useDragAndDrop } from "@formkit/drag-and-drop/vue";
import { ref } from "vue";

const items = ref(
  Array.from({ length: 40 })
    .fill(0)
    .map((_, i) => ({
      name: `Item ${i + 1}`,
      pinPosition: i % 2 === 0 ? i : null,
      id: i,
    }))
);
const [parent, list] = useDragAndDrop(items.value, {
  nativeDrag: false,
  synthDropZoneClass: "placeholder",
  synthDraggingClass: "dragging",
  longPress: true,
  longPressDuration: 200,
});
</script>

<template>
  <div class="note">
    <code>
      Apply a "touch-action: none" style to each item to disable the default
      scroll behavior on mobile devices. Let's try swiping gestures to scroll.
    </code>
  </div>
  <br />
  <div class="container">
    <ul ref="parent" class="grid">
      <li v-for="item in list" :key="item.id" class="grid-item">
        <div>{{ item.name }}</div>
      </li>
    </ul>
  </div>
</template>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 0.5rem;
  padding: 0;
  width: 100%;
  justify-items: center;
  margin-top: 0;
}

.grid-item {
  background: #4caf50;
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
}

.placeholder {
  opacity: 0;
}

.dragging {
  transform: scale(1.1);
  opacity: 0.5;
}
</style>
