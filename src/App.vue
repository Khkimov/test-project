<template>
  <div class="container">
    <!-- Верхние блоки -->
    <div class="top-blocks">
      <!-- Выбранные вещи пользователя -->
      <div class="selected-items">
        <h2>Выбранные вещи пользователя</h2>
        <div class="items-container">
          <div v-for="item in selectedUserItems"
               :key="item.id"
               class="item">
            {{ item.name }}
          </div>
        </div>
      </div>

      <!-- Выбранная вещь из предложенных -->
      <div class="selected-item">
        <h2>Выбранная вещь</h2>
        <div class="items-container">
          <div v-if="selectedProposedItem"
               class="item">
            {{ selectedProposedItem.name }}
          </div>
          <div v-else class="placeholder">
            Нет выбранной вещи
          </div>
        </div>
      </div>
    </div>

    <!-- Нижние блоки -->
    <div class="bottom-blocks">
      <!-- Вещи пользователя -->
      <div class="user-items">
        <h2>Вещи пользователя</h2>
        <div class="items-container">
          <div v-for="item in userItems"
               :key="item.id"
               class="item"
               @click="handleUserItemClick(item)">
            {{ item.name }}
          </div>
        </div>
      </div>

      <!-- Предложенные вещи -->
      <div class="proposed-items">
        <h2>Предложенные вещи</h2>
        <div class="items-container">
          <div v-for="item in proposedItems"
               :key="item.id"
               class="item"
               @click="handleProposedItemClick(item)">
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";

interface Item {
  id: number;
  name: string;
}

const userItems = ref<Item[]>([
  { id: 1, name: "Shoes 1" },
  { id: 2, name: "Shoes 2" },
  { id: 3, name: "Shoes 3" },
  { id: 4, name: "Shoes 4" },
  { id: 5, name: "T-shirt 1" },
  { id: 6, name: "T-shirt 2" },
  { id: 7, name: "T-shirt 3" },
  { id: 8, name: "T-shirt 4" }
]);

const proposedItems = ref<Item[]>([
  { id: 11, name: "Jacket 1" },
  { id: 12, name: "Jacket 2" },
  { id: 13, name: "Jacket 3" },
  { id: 14, name: "Jacket 4" },
  { id: 15, name: "Hoodie 1" },
  { id: 16, name: "Hoodie 2" },
  { id: 17, name: "Hoodie 3" },
  { id: 18, name: "Hoodie 4" }
]);

const selectedUserItems = ref<Item[]>([]);
const selectedProposedItem = ref<Item | null>(null);

const handleUserItemClick = (item: Item) => {
  if (selectedUserItems.value.length >= 6) {
    alert('Можно выбрать не более 6 вещей');
    return;
  }

  if (!selectedUserItems.value.some(i => i.id === item.id)) {
    selectedUserItems.value.push(item);
  }
};

const handleProposedItemClick = (item: Item) => {
  selectedProposedItem.value = item;
};
</script>