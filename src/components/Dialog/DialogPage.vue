<template>
  <q-dialog v-model="confirm" persistent>
    <q-card>
      <q-card-section class="row items-center">
        <span class="q-ml-sm"
          >Было бы здорово провести время вместе! Как ты на это смотришь?</span
        >
      </q-card-section>
      <q-card-actions align="center">
        <q-btn
          no-caps
          flat
          label="Не согласна"
          color="negative"
          @click="negativeAnswer"
        />
        <q-btn
          no-caps
          flat
          label="Согласна"
          color="positive"
          @click="positiveAnswer"
        />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script setup>
import { QSpinnerInfinity, useQuasar } from "quasar";
import { ref, watch } from "vue";

const $q = useQuasar();
const props = defineProps({
  openPage: {
    type: Boolean,
    required: true,
  },
});

const confirm = ref(props.openPage);

watch(
  () => props.openPage,
  (newVal) => {
    confirm.value = newVal;
  }
);

const negativeAnswer = () => {
  $q.notify({
    message: "Неправильный ответ!",
    color: "negative",
    icon: "error",
  });
};

const positiveAnswer = () => {
  $q.notify({
    message: "Прекрасный ответ!",
    color: "positive",
    spinner: QSpinnerInfinity,
  });
};
</script>

<style></style>
