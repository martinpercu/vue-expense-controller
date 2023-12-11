<script setup>
const currencyFormat = new Intl.NumberFormat('fr-FR', {
    currency: "EUR",
    style: "currency",
});


import { toRefs, computed } from 'vue';

const props = defineProps({
    id: {
        type: Number
    },
    title: {
        type: String,
    },
    description: {
        type: String,
    },
    amount: {
        type: Number,
    }
});

const { id, title, description, amount } = toRefs(props);

const amountCurrency = computed(() => currencyFormat.format(amount.value));

const emit = defineEmits(["removeExpense"]);

const isPositive = computed(() => amount.value > 0);

const removeExpense = () => {
    emit("removeThisExpense", id.value);
    console.log("this is id value ==> " + id.value);
}

</script>

<template>
    <div class="expense">
        <div class="content">
            <h4>{{ title }}</h4>
            <p>{{ description }}</p>
        </div>
        <div class="action">
            <font-awesome-icon :icon="['fas', 'trash']"  @click="removeExpense" />
            <p :class="[{ 'green': isPositive, 'red': !isPositive }]">{{ amountCurrency }}</p>
        </div>
    </div>
</template>


<style scoped>
.expense {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background: rgb(246,248,255);
  background: linear-gradient(135deg, rgba(246,248,255,1) 0%, rgba(242,255,246,1) 100%);
  border-radius: 8px;
  box-sizing: border-box;
  border: 1px solid lightgray;
}

.expense .content {
  width: 100%;
}

.expense .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.expense .action svg {
  margin-bottom: 20px;
}

.red {
    color: rgb(214, 38, 38);
}

.green {
    color: rgb(8, 84, 8);
}
</style>