<template>
  <div :class="item.status === `green` ? 'green' : `red`" class="block lk__data-card">
    <p>
      {{ item.status === "green" ? "Задача выполнена:" : "Задача в работе" }}
      <span class="text-bold">{{ item.date }}</span>
    </p>
    <p>
      Статус задачи: <span class="text-bold">{{ item.status_text }}</span>
    </p>
    <p>
      ID выгрузки: <span class="text-bold">{{ item.id }}</span>
    </p>
    <p>{{ props.event }}</p>
    <p>
      Размер выгрузки: <span class="text-bold">{{ item.size }}</span>
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true
  }
});
</script>
