<template>
  <main class="lk__layout">
    <div class="lk__left">
      <LkType
        ><h5 class="text-bold">Выгрузка</h5>
        <p class="text-bold">Выполняет работу:</p>
        <p>- Собирает фотографии из заказов пользователей.</p>
        <p>- Выгружает по папкам.</p></LkType
      >
      <LkDataCard v-for="item in allItems" :key="item.id" @click="getOne(item)" :item="item" />
      <p v-if="!allItems.length" style="font-size: 30px">Идёт загрузка</p>
    </div>
    <div class="lk__right">
      <LkActiveItem v-if="activeItem" v-model:show="activeItem" :activeItem="activeItem" />
      <div v-else class="notice" data-color="light-purple">
        Для того, чтобы посмотреть информацию о <span class="text-bold">выгрузке</span>, а также её скачать, нажмите на
        требуемую выгрузку в столбце слева
      </div>
    </div>
  </main>
</template>

<script setup>
const allItems = ref([]);
const activeItem = ref(null);

const getAll = async () => {
  await nextTick();
  const request = await useAPIFetch("https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get");
  const parsed = JSON.parse(request?.data?.value);
  allItems.value = parsed?.response?.data || [];
};

const getOne = async item => {
  const request = await useAPIFetch(`https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get&unload_i
d=${item.id}`);
  const parsed = JSON.parse(request?.data?.value);

  activeItem.value = parsed?.response?.data[0] || [];
};

onMounted(getAll);
</script>
