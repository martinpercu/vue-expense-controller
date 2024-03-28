<script setup>
const emit = defineEmits(["closeModal"]);

const closeModal = () => emit("closeModal");

</script>

<template>
    <div class="modal">
        <div class="header">
            <p>New expense</p>
            <font-awesome-icon :icon="['fas', 'close']" @click="closeModal" />
        </div>
        <div class="body">
            <slot>

            </slot>
        </div>
        
    </div>
</template>


<style scoped>
.modal {
  z-index: 3;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: white;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 24px;
  box-sizing: border-box;
}

.header svg {
    color: var(--brand-blue);
}

p {
  margin: 0;
  font-size: 1.5rem;
  color: var(--brand-blue);
}
</style>