<template>
  <v-app>
    <v-main>
      <body>
        <div class="container">
          <header>
            <h1>I.R.I.N.App</h1>
            <div сlass="heading">
              <h2>Введите сумму договора (используйте точку)</h2>
              <v-text-field
                v-model="price"
                placeholder="Сумма договора"
                size="30"
              />
            </div>
          </header>

          <div class="results">
            <h2>{{ rubles(price) }}</h2>
            <div class="title">
              <span>Наименование</span><span>Цифровое значение</span
              ><span>Буквенное значение</span>
            </div>
            <div class="row">
              <span>НДС 20%</span
              ><span>{{ nds.toString().replace(".", ",") }}</span
              ><span>{{ rubles(nds) }}</span>
            </div>

            <div class="row">
              <span>Аванс 30%</span
              ><span>{{ advance.toString().replace(".", ",") }}</span
              ><span>{{ rubles(advance) }}</span>
            </div>
            <div class="row">
              <span>НДС 20% от аванса</span
              ><span>{{ ndsAdvance.toString().replace(".", ",") }}</span
              ><span>{{ rubles(ndsAdvance) }}</span>
            </div>

            <div class="row">
              <span>Остаток 70%</span
              ><span>{{ rest.toString().replace(".", ",") }}</span
              ><span>{{ rubles(rest) }}</span>
            </div>
            <div class="row">
              <span>НДС 20% от остатка</span
              ><span>{{ ndsRest.toString().replace(".", ",") }}</span
              ><span>{{ rubles(ndsRest) }}</span>
            </div>

            <div class="row">
              <span>10%</span
              ><span>{{ tenPersents.toString().replace(".", ",") }}</span
              ><span>{{ rubles(tenPersents) }}</span>
            </div>

            <div class="row">
              <span>5%</span
              ><span>{{ fivePersents.toString().replace(".", ",") }}</span
              ><span>{{ rubles(fivePersents) }}</span>
            </div>

            <div class="row">
              <span>2.5%</span
              ><span>{{ twoPersents.toString().replace(".", ",") }}</span
              ><span>{{ rubles(twoPersents) }}</span>
            </div>
          </div>
        </div>
      </body>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, watch } from "vue";
import { rubles } from "rubles";
import Decimal from "decimal.js";

const price = ref("");
let tenPersents = ref("");
let fivePersents = ref("");
let twoPersents = ref("");
let nds = ref("");
let advance = ref("");
let rest = ref("");
let ndsAdvance = ref("");
let ndsRest = ref("");

watch(price, (newValue) => {
  tenPersents.value = Decimal(newValue).dividedBy(100).times(10).toFixed(2);
});

watch(price, (newValue) => {
  advance.value = Decimal(newValue).dividedBy(100).times(30).toFixed(2);
});

watch(price, (newValue) => {
  rest.value = Decimal(newValue).dividedBy(100).times(70).toFixed(2);
});

watch(price, (newValue) => {
  fivePersents.value = Decimal(newValue).dividedBy(100).times(5).toFixed(2);
});

watch(price, (newValue) => {
  twoPersents.value = Decimal(newValue).dividedBy(100).times(2.5).toFixed(2);
});

watch(price, (newValue) => {
  nds.value = Decimal(newValue).times(20).dividedBy(120).toFixed(2);
});

watch(advance, (newValue) => {
  ndsAdvance.value = Decimal(newValue).times(20).dividedBy(120).toFixed(2);
});

watch(rest, (newValue) => {
  ndsRest.value = Decimal(newValue).times(20).dividedBy(120).toFixed(2);
});
</script>

<style lang="css" scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 30px;
  width: 100%;
}

h1,
h2 {
  text-align: center;
}

h2 {
  margin-bottom: 15px;
}

header {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.row {
  display: flex;
  width: 100%;
  justify-content: space-between;
  border: 1px solid rgb(98, 255, 182);
  border-radius: 10px;
  padding: 5px;
}

.title {
  display: flex;
  width: 100%;
  justify-content: space-between;
  padding: 5px;
  background-color: rgb(98, 255, 182);
  border-radius: 10px;
}

span {
  font-size: 20px;
  font-weight: 600;
}

span:first-child,
span:nth-child(2) {
  min-width: 25%;
  font-size: 20px;
  font-weight: 600;
}

span:last-child {
  min-width: 50%;
  font-size: 20px;
  font-weight: 600;
}

.results {
  display: flex;
  flex-direction: column;
  min-width: 100%;
  gap: 20px;
  padding: 0 20;
}

input {
  font-size: 40px;
}
</style>
