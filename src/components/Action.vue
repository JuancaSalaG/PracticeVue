<template>
    <button @click="showModal = true">Agregar movimiento</button>
    <teleport to='#app'>
        <Modal v-show="showModal" @close="showModal = false">
            <form @submit.prevent="submit">
                <div class="field">
                    <label for="title">Título</label>
                    <input type="text" id="title" v-model="title" />
                </div>
                <div class="field">
                    <label for="description">Descripción</label>
                    <textarea rows="4" id="description" v-model="description"></textarea>
                </div>
                <div class="field">
                    <label for="amount">Monto</label>
                    <input type="number" id="amount" v-model="amount"/>
                </div>
                <div class="field">
                    <label for="income" class="radio-label">
                        <input id="income" type="radio" v-model="movementType" value="Ingreso">
                        <span>Ingreso</span>
                    </label>
                </div>
                <div class="field">
                    <label for="spend" class="radio-label">
                        <input id="spend" type="radio" v-model="movementType" value="Gasto">
                        <span>Gasto</span>
                    </label>
                </div>
                <div class="action">
                    <button type="submit">Agregar movimiento</button>
                </div>
            </form>
        </Modal>
    </teleport>
</template>

<script setup>
import Modal from "@/components/Modal.vue";
import { ref } from "vue";

const showModal = ref(false);
const title = ref("");
const description = ref("");
const amount = ref(0);
const movementType = ref("Ingreso");

const emit = defineEmits(["create"]);

const submit = () => {
  showModal.value = false;
  emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Gasto" ? -amount.value : amount.value,
    type: movementType.value,
    time: new Date()
  });
  title.value = "";
  description.value = "";
  amount.value = 0;
  movementType.value = "Ingreso";
};
</script>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
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
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>