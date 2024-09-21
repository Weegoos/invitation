<template>
  <div>Batyr</div>
</template>

<script setup>
import { useQuasar } from "quasar";
const name = "Batyr";
sessionStorage.setItem("name", name);
const $q = useQuasar();
const sessionStorageName = sessionStorage.getItem("name");
$q.notify({
  message: sessionStorageName,
});
</script>
