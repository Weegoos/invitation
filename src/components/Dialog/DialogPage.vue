<template>
  <q-dialog v-model="confirm" persistent>
    <q-card v-if="isAgree">
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
    <q-card v-if="card" class="my-card q-pa-md" style="width: 100vw">
      <p class="text-h5 text-bold">Планирование</p>
      <form action="">
        <q-select
          v-model="day"
          :options="dayOptions"
          multiple
          label="Выберите дни когда можете встретиться"
          filled
        />
        <q-select
          v-model="time"
          :options="timeOptions"
          multiple
          class="q-mt-md"
          label="Выберите время когда можете встретиться"
          filled
          required
        />
        <q-input
          v-model="interests"
          autogrow
          type="text"
          label="Напишите ваши предпочтение и интересы"
          filled
          class="q-mt-md"
          required
        />
      </form>
      <q-card-actions align="right">
        <q-btn
          class="q-mt-md"
          color="positive"
          no-caps
          label="Завершить"
          @click="submitData"
        />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script setup>
import { QSpinnerInfinity, useQuasar } from "quasar";
import { ref, watch } from "vue";
import { useRouter } from "vue-router";

const $q = useQuasar();
const card = ref(false);
const props = defineProps({
  openPage: {
    type: Boolean,
    required: true,
  },
});

const day = ref(null);
const time = ref(null);
const interests = ref("");
const router = useRouter();

const submitData = () => {
  if (day.value != null && time.value != null && interests.value.length > 0) {
    $q.notify({
      message: "Отлично! Желаю хорошего настроение!",
      color: "positive",
    });
    sessionStorage.setItem("day", day.value);
    sessionStorage.setItem("time", time.value);
    sessionStorage.setItem("interests", interests.value);

    setTimeout(() => {
      router.push("/result");
    }, 2500);
  } else {
    $q.notify({
      message: "Вы не заполнили все поля",
      color: "secondary",
    });
  }
};

const dayOptions = [
  "Вторник",
  "Среда",
  "Четверг",
  "Пятница",
  "Суббота",
  "Воскресенье",
];

const timeOptions = [
  "19:00 - 20:00",
  "20:00 - 21:00",
  "21:00 - 22:00",
  "Другое",
];
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

const isAgree = ref(true);
const positiveAnswer = () => {
  $q.notify({
    message: "Прекрасный ответ!",
    color: "positive",
    spinner: QSpinnerInfinity,
  });
  isAgree.value = false;
  card.value = true;
  sessionStorage.setItem("agree", isAgree.value);
  console.log(isAgree.value);
};

const isSheAgreeSession = sessionStorage.getItem("agree");
if (isSheAgreeSession === "false") {
  isAgree.value = false;
  card.value = true;
}
</script>

<style></style>
