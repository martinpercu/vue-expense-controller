<script setup>
import { ref } from "vue";
import Modal from "./Modal.vue"

const showModal = ref(false)

const title = ref("");
const amount = ref(0);
const description = ref("");
const expenseType = ref("expense");


const emit = defineEmits(["sendNewExpense"]);

const submit = () => {
    showModal.value = !showModal.value;
    emit("sendNewExpense", {
        id: 654,
        title: title.value,
        description: description.value,
        amount: expenseType.value === "income" ? amount.value : -amount.value,
        time: new Date(),
    });
}


</script>

<template>
    <button @click="showModal = true">Add expense</button>
    <teleport to='#app'>
        <Modal v-show="showModal" @closeModal="showModal = false">
            <form @submit.prevent="submit">
                <div class="field">
                    <label>Title</label>
                    <input type="text" v-model="title">
                </div>
                <div class="field">
                    <label>Amount</label>
                    <input type="number" v-model="amount">
                </div>
                <div class="field">
                    <label>Description</label>
                    <textarea row="3" v-model="description"></textarea>
                </div>
                <div class="field radioField">
                    <label class="radio-label">
                        <input type="radio" v-model="expenseType" value="expense">
                        <span class="spanExpense">Expense</span>
                    </label>
                    <label class="radio-label">
                        <input type="radio" v-model="expenseType" value="income">
                        <span class="spanIncome">Income</span>
                    </label>
                </div>
                <div class="action">
                    <button>Add</button>
                </div>
            </form>
        </Modal>
    </teleport>
</template>


<style scoped>
button {
    color: white;
    font-size: 1.25rem;
    background-color: var(--brand-blue);
    border: none;
    width: 100%;
    padding: 16px 50px;
    border-radius: 20px;
    box-sizing: border-box;
}

form {
    font-size: 1.24rem;
    width: 100%;
}

form .action {
    padding: 0 24px;
}

.field {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    padding: 8px 24px;
}

.radioField {
    display: block;
    display: flex;
    flex-direction: row;
    padding-bottom: 16px;
}


label {
    margin-bottom: 8px;
}

input,
textarea {
    font-size: 1.24rem;
    border: 2px solid var(--brand-blue-light);
    border-radius: 8px;
    padding: 8px;
}

textarea {
    height: 16vh;
}


input[type="number"] {
    text-align: right;
}

.radio-label {
    margin-top: 18px;
    margin-bottom: 18px;
    width: 50%;
    text-align: center;
}

.radio-label span {
    margin-top: 4px;
    margin-left: 8px;
    color: var(--brand-blue);
}

input[type="radio"] {
    appearance: none;
    width: 1.24rem;
    height: 1.24rem;
    border-radius: 50%;
    position: relative;
    top: 3px;
}

input[type="radio"]:checked {
    background-color: var(--brand-blue);
}


</style>