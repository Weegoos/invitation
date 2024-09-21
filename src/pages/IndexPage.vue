<template>
  <div>
    <q-img
      src="../assets/main/invitationMainImg.jpg"
      style="width: 100vw; height: 100vh"
      spinner-color="primary"
      spinner-size="82px"
    >
      <div class="absolute-center bg-transparent">
        <q-btn no-caps color="secondary" label="Начать" @click="start" />
      </div>
    </q-img>
    <DialogPage :openPage="openPage" />
  </div>
</template>

<script setup>
import { QSpinnerGears, useQuasar } from "quasar";
import { ref } from "vue";
import DialogPage from "../components/Dialog/DialogPage.vue";
const $q = useQuasar();

$q.notify({
  message: "Добро пожаловать, Камила!",
  icon: "check",
  color: "positive",
  timeout: 2500,
});

$q.notify({
  message: "Нажмите на кнопку Начать",
  timeout: 7000,
  spinner: QSpinnerGears,
});

const openPage = ref(false);
const start = () => {
  openPage.value = true;
};
</script>
