<script setup>
import { toRefs } from 'vue';
import Expense from './Expense.vue';

const props = defineProps({
  theExpenses: {
        type: Array,
        default: () => [],
    }
});

const { theExpenses } = toRefs(props);

const emit = defineEmits(["removeThisExpense"]);

const removeThis = (id) => {
  console.log("remove", id);
  emit("removeThisExpense", id);
};

</script>

<template>
    <div class="history">
        <h2 class="title">History</h2>
        <div class="content">
            <Expense 
                v-for="{ id, title, description, amount } in theExpenses" 
                :key="id"
                :id="id"
                :title="title"
                :description="description"
                :amount="amount"
                @removeThisExpense="removeThis"
              />
        </div>   
    </div>
</template>

<style scoped>
.history {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}

.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}

.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>