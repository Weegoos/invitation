<template>
  <div>
    <q-img
      src="../assets/main/result.jpg"
      style="width: 100vw; height: 100vh"
      spinner-color="primary"
      spinner-size="82px"
    >
      <div class="absolute-center bg-transparent">
        <q-dialog
          v-model="confirm"
          persistent
          style="width: 100%; overflow: hidden"
        >
          <q-card>
            <q-card-section class="items-center" style="width: 100%">
              <p class="text-bold text-body1">
                Отлично! Мы запланировали день/дни встречи.
              </p>
              <div style="display: block">
                <span class="text-bold">Вы выбрали эту дату: </span>
                <span>{{ day }}</span>
              </div>
              <div>
                <span class="text-bold">Вы выбрали это время: </span>
                <span>{{ time }}</span>
              </div>
              <div>
                <span class="text-bold"> Ваши предпочтение: </span>
                <span>{{ interests }}</span>
              </div>
            </q-card-section>
            <q-card-actions align="right">
              <!-- <q-btn flat label="Cancel" color="primary" v-close-popup />
              <q-btn flat label="Turn on Wifi" color="primary" v-close-popup /> -->
            </q-card-actions>
          </q-card>
        </q-dialog>
      </div>
    </q-img>
  </div>
</template>

<script setup>
import { ref } from "vue";

const confirm = ref(true);
const day = sessionStorage.getItem("day");
const time = sessionStorage.getItem("time");
const interests = sessionStorage.getItem("interests");
</script>

<style></style>
