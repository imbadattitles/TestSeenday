<template>
  <main class="lk__layout">
    <div class="lk__right">
      <div class="block lk__type">
        <h5 class="text-bold">Выгрузка</h5>
        <p class="text-bold">Выполняет работу:</p>
        <p>- Собирает фотографии из заказов пользователей.</p>
        <p>- Выгружает по папкам.</p>
      </div>
      <div v-if="allItems.length">
        <div v-for="item in allItems" :key="item.id" :on-click="chooseItem" class="block lk__data-card">
          <p>Задача выполнена: <span class="text-bold">15.09.2023 в 02:04 (GMT)</span></p>
          <p>Статус задачи: <span class="text-bold">Выгрузка успешно завершена</span></p>
          <p>ID выгрузки: <span class="text-bold">64</span></p>
          <p>Выгрузка заказа из фотосессии: <span class="text-bold">№ 4935</span></p>
          <p>Размер выгрузки: <span class="text-bold">1.6 MiB</span></p>
        </div>
      </div>
    </div>

    <div class="lk__left">
      <!-- <div class="notice" data-color="light-purple">
        Для того, чтобы посмотреть информацию о <span class="text-bold">выгрузке</span>, а также её скачать, нажмите на
        требуемую выгрузку в столбце слева
      </div> -->
      <div class="lk__active block">
        <div class="lk__activeTop">
          <p class="lk__activeTop-id">63</p>
          <p class="lk__activeTop-title">Выгрузка заказа из фотосессии: № 4935</p>
          <span class="lk__activeTop-close"></span>
        </div>
        <div class="lk__activeBtm">
          <div class="lk__activeBtm-alert">
            Если после клика на ссылку загрузка не началась, проверьте, не блокирует ли браузер скачивание архива
          </div>
          <p class="text-bold">Ссылка для скачивания архива Выгрузки (.zip):</p>
          <div class="lk__activeBtm-link link">
            <a>sdfsdfsdferwr</a> <span class="span-link">Скопировать ссылку</span>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
// import { on } from "events";

const allItems = ref([]);
const activeItem = ref(null);

const chooseItem = item => {
  activeItem.value = item.id;
};

// const { data } = await useAPIFetch("https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get");

const getAll = async () => {
  const { data } = await useAPIFetch("https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get");
  const parse = await JSON.parse(data.value);
  allItems.value = await parse.response.data;
  // console.log(allItems.value);
};

onMounted(getAll);
</script>
