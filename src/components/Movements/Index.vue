<template>
    <div class="movements">
        <h2 class="title">Historial</h2>
        <div class="content">
            <Movement
                v-for="{ id, title, description, amount } in movements" 
                :key="id"
                :title="title"
                :description="description"
                :amount="amount"
                :id="id"
                @remove="removeMovement"
            />
        </div>
    </div>
</template>

<script setup>
import Movement from "./Movement.vue";
import { toRefs, defineProps } from "vue";

const props = defineProps({
    movements: {
        type: Array,
        required: true,
        default: () => [],
    }
});

const { movements } = toRefs(props);
const emit = defineEmits(["remove"]);

const removeMovement = (id) => {
    emit("remove", id);
}
</script>

<style scoped>
.movements {
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