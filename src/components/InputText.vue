<script>
export default {
  name: 'InputText',
  props: {
    id: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'input'
    },
    name: {
      type: String,
      default: ''
    },
    modelValue: {
      type: String,
      default: ''
    },
    maxLength: {
      type: Number,
      default: undefined
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      showError: false,
      errorMessage: ''
    };
  },
  methods: {
    /**
     * Resets the error state to the default (no error, message content is empty).
     */
    clearError() {
      this.showError = false;
      this.errorMessage = '';
    },

    /**
     * Marks input as having an error. Adds the specified message below it.
     *
     * @param {string} message - Message content
     */
    setError(message) {
      this.showError = true;
      this.errorMessage = message;
    }
  }
};
</script>

<template>
  <div
    class="input-text"
    :class="{ 'error' : showError }"
  >
    <p v-show="showError && errorMessage" class="error-message">
      {{ errorMessage }}
    </p>
    <input
      v-if="type === 'input'"
      :id="id"
      type="text"
      :maxlength="maxLength"
      :disabled="disabled"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <textarea 
      v-else
      :id="id"
      :name="name" 
      cols="30" 
      rows="10"
      :maxlength="maxLength"
      :disabled="disabled"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>
</template>