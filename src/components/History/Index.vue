<script setup>
import { toRefs } from 'vue';
import Expense from './expense.vue';
const props = defineProps({
    expenses: {
        type: Array,
        default: () => []
    }
});

const { expenses } = toRefs(props);

const removeThis = (id) => {
  console.log("remove", id);
};

</script>

<template>
    <div class="history">
        <h2 class="title">History</h2>
        <div class="content">
            <Expense 
                v-for="{ id, title, description, amount } in expenses" 
                :key="id"
                :id="id"
                :title="title"
                :description="description"
                :amount="amount"
                @removeThisExpense="removeThis"
              >    
            </Expense>
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