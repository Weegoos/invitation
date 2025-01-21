<template>
  <q-dialog v-model="confirm" persistent>
    <q-card v-if="isAgree">
      <q-card-section>
        <p class="text-h6 text-bold text-center">Приглашение на свидание</p>
        <span class="text-center"
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
          label="Выберите дни и время когда сможете встретиться"
          filled
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
const interests = ref("");
const router = useRouter();

const submitData = () => {
  if (day.value != null && interests.value.length > 0) {
    $q.notify({
      message: "Отлично! Желаю хорошего настроение!",
      color: "positive",
    });
    sessionStorage.setItem("day", day.value);
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
  "25.01.2025 (До обеда)",
  "25.01.2025 (После обеда)",
  "25.01.2025 (В любое время)",
  "26.01.2025 (До обеда)",
  "26.01.2025 (После обеда)",
  "26.01.2025 (В любое время)",
  "01.02.2025",
  "02.02.2025",
  "08.02.2025",
  "09.02.2025",
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
