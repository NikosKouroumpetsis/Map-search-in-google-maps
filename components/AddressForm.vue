<template>
  <div>
    <div>
      <label for="address">Διεύθυνση:</label>
      <input
        type="text"
        id="address"
        v-model="localForm.address"
        @input="updateForm"
        class="inputStyle"
        @blur="$emit('addressBlur')"
      />
    </div>
    <div>
      <label for="address">Αριθμός:</label>
      <input
        type="text"
        id="address_number"
        v-model="localForm.addressNumber"
        @input="updateForm"
        class="inputStyle"
      />
    </div>
    <div>
      <label for="address">state</label>
      <input
        type="text"
        id="state"
        v-model="localForm.state"
        @input="updateForm"
        class="inputStyle"
      />
    </div>
    <div>
      <label for="address">city</label>
      <input
        type="text"
        id="city"
        v-model="localForm.city"
        @input="updateForm"
        class="inputStyle"
      />
    </div>
    <div>
      <label for="address">postcode</label>
      <input
        type="text"
        id="postcode"
        v-model="localForm.postcode"
        @input="updateForm"
        class="inputStyle"
      />
    </div>
    <div>
      <label for="address">floor</label>
      <input
        type="text"
        id="floor"
        v-model="localForm.floor"
        @input="updateForm"
        class="inputStyle"
      />
    </div>
    <!-- Παρόμοιος κώδικας για τα υπόλοιπα πεδία -->
  </div>
</template>

<script setup lang="ts">
import type { AddressFormType } from "../app.vue";

const props = defineProps<{
  form: AddressFormType;
}>();

const localForm = ref<AddressFormType>({ ...props.form });

watch(props.form, (newForm) => {
  localForm.value = { ...newForm };
});

const emit = defineEmits(["form", "submit", "addressBlur"]);

const updateForm = () => {
  emit("form", localForm.value);
};

const onSubmit = () => {
  emit("submit");
};
</script>

<style scoped>
.inputStyle {
  @apply bg-gray-50 border border-gray-300 rounded-lg;
}
</style>
