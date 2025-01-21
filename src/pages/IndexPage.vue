<template>
  <div>
    <q-img
      src="../assets/main/rose.jpg"
      style="width: 100vw; height: 100vh"
      spinner-color="primary"
      spinner-size="82px"
      @load="onImageLoad"
    >
      <div class="absolute-center bg-transparent">
        <q-btn
          v-if="imageLoaded"
          no-caps
          color="secondary"
          label="Начать"
          @click="start"
        />
      </div>
    </q-img>
    <DialogPage :openPage="openPage" />
  </div>
</template>

<script setup>
import { QSpinnerGears, useQuasar } from "quasar";
import { onMounted, ref } from "vue";
import DialogPage from "../components/Dialog/DialogPage.vue";

const $q = useQuasar();

const isSheAgreeSession = sessionStorage.getItem("agree");
onMounted(() => {
  checkStatus();
});
const checkStatus = () => {
  if (isSheAgreeSession === null) {
    $q.notify({
      message: "Добро пожаловать, Assem!",
      icon: "cloud_done",
      color: "positive",
      timeout: 5000,
    });
  }
};

$q.notify({
  message: "Нажмите на кнопку Начать",
  timeout: 7000,
  spinner: QSpinnerGears,
});

const openPage = ref(false);
const imageLoaded = ref(false); // Флаг для отслеживания загрузки изображения

const start = () => {
  openPage.value = true;
};

const onImageLoad = () => {
  imageLoaded.value = true; // Устанавливаем флаг в true после загрузки изображения
};
</script>
