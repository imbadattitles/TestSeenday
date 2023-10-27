<template>
  <div v-if="activeItem" class="lk__active block">
    <div class="lk__activeTop">
      <p class="lk__activeTop-id">{{ activeItem.id }}</p>
      <p class="lk__activeTop-title">{{ activeItem.event }}</p>
      <span @click="hide" class="lk__activeTop-close"></span>
    </div>
    <div class="lk__activeBtm">
      <div class="lk__activeBtm-alert">
        Если после клика на ссылку загрузка не началась, проверьте, не блокирует ли браузер скачивание архива
      </div>
      <p class="text-bold">Ссылка для скачивания архива Выгрузки (.zip):</p>
      <div class="lk__activeBtm-link link">
        <a>{{ activeItem.download_link }}</a>
        <span @click="copyText" class="span-link">Скопировать ссылку</span>
      </div>
    </div>
  </div>
</template>
<script setup>
const emit = defineEmits(["update:show"]);
const hide = () => {
  emit("update:show", null);
};

const props = defineProps({
  activeItem: {
    required: true,
    type: Object
  }
});

const copyText = async () => {
  try {
    await navigator.clipboard.writeText(props.activeItem.download_link);
  } catch (err) {
    console.log("Copy failed!");
  }
};
</script>
<style lang=""></style>
