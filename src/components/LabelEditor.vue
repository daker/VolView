<script setup lang="ts">
import { toRefs } from 'vue';

const emit = defineEmits(['done', 'cancel', 'delete', 'update:color']);
const props = defineProps({
  color: String,
});
const { color } = toRefs(props);

const done = () => {
  emit('done');
};

const cancel = () => {
  emit('cancel');
};

const onDelete = () => {
  emit('delete');
  emit('done');
};
</script>

<template>
  <v-card>
    <slot name="title"></slot>
    <v-card-item>
      <div class="d-flex flex-row">
        <div class="flex-grow-1 d-flex flex-column justify-space-between mr-4">
          <slot name="fields" :done="done"></slot>
          <v-card-actions class="mb-2 px-0">
            <v-btn color="error" variant="elevated" @click="onDelete">
              Delete
            </v-btn>
            <v-spacer />
            <v-btn color="cancel" variant="tonal" @click="cancel">
              Cancel
            </v-btn>
            <v-btn
              color="secondary"
              variant="elevated"
              @click="done"
              data-testid="edit-label-done-button"
            >
              Done
            </v-btn>
          </v-card-actions>
        </div>
        <v-color-picker
          :model-value="color"
          @update:model-value="$emit('update:color', $event)"
          mode="rgb"
          label="Color"
        />
      </div>
    </v-card-item>
  </v-card>
</template>
