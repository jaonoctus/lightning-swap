<script setup lang="ts">
import { ref, computed, onBeforeMount } from "vue";

const MIN_AMOUNT = 10_000;

const isServiceAvailable = ref(false);
const amount = ref(MIN_AMOUNT);
const address = ref("");
const feeRate = ref(1);

const isButtonDisabled = computed(() => {
  if (isServiceAvailable.value === false) {
    return true;
  }

  // validate amount
  if (amount.value < MIN_AMOUNT) {
    return true;
  }

  // validate address
  if (address.value === "") {
    return true;
  }

  return false;
});

const totalAmount = computed(() => {
  return amount.value; // TODO: sum fee
});

onBeforeMount(async () => {
  console.log("call api");
  isServiceAvailable.value = true;
});

function onSubmit() {
  console.log({
    amount: amount.value,
    address: address.value,
    feeRate: feeRate.value,
  });
}
</script>

<template>
  <div>
    <form>
      <div>
        <input v-model="amount" type="number" :min="MIN_AMOUNT" step="1" />
      </div>
      <div>
        <input v-model="address" type="text" />
      </div>
      <div>
        <input v-model="feeRate" type="range" min="1" max="100" />
      </div>
      <div>
        <div>{{ feeRate }} sat/vB</div>
        <div>total: {{ totalAmount }} sats</div>
      </div>
      <div>
        <button
          @click.prevent="onSubmit"
          :disabled="isButtonDisabled"
          type="submit"
        >
          Continue
        </button>
      </div>
    </form>
  </div>
</template>

<style scoped>
form {
  display: block;
}
</style>
