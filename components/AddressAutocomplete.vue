<template>
  <div>
    <input
      type="text"
      v-model="address"
      @input="onInput"
      class="w-full p-2"
      placeholder="Εισάγετε διεύθυνση"
    />
    <div v-if="pending">Φόρτωση...</div>
    <div v-else-if="suggestions.length" class="mt-2">
      <div
        v-for="suggestion in suggestions"
        :key="suggestion.place_id"
        @click="selectSuggestion(suggestion.place_id)"
      >
        {{ suggestion.description }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { suggestions, pending } = defineProps<{
  suggestions: { place_id: string; description: string }[];
  pending: boolean;
}>();
const address = ref("");

const emit = defineEmits<{
  (event: "input", value: string): void;
  (event: "select", value: string): void;
}>();
const onInput = () => {
  emit("input", address.value);
};

const selectSuggestion = (placeId: string) => {
  emit("select", placeId);
};
</script>
