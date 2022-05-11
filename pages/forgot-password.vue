<template>
  <div>
    <div class="mb-4 text-sm text-gray-600">
      Forgot your password? No problem. Just let us know your email address and
      we will email you a password reset link that will allow you to choose a
      new one.
    </div>

    <!-- Validation Errors -->
    <BreezeValidationErrors :errors="form.errors" class="mb-4" />

    <form @submit.prevent="submit">
      <div>
        <BreezeLabel for="email" value="Email" />
        <BreezeInput
          id="email"
          type="email"
          class="mt-1 block w-full"
          v-model="form.email"
          required
          autofocus
          autocomplete="username"
        />
      </div>

      <div class="flex items-center justify-end mt-4">
        <BreezeButton
          :class="{ 'opacity-25': form.processing }"
          :disabled="form.processing"
        >
          Email Password Reset Link
        </BreezeButton>
      </div>
    </form>
  </div>
</template>

<script>
import BreezeValidationErrors from "@/components/validation-errors.vue";
import BreezeButton from "@/components/button.vue";
import BreezeInput from "@/components/input.vue";
import BreezeLabel from "@/components/label.vue";
export default {
  head: {
    title: "Forgot Password",
  },

  layout: "guest",

  components: {
    BreezeValidationErrors,
    BreezeButton,
    BreezeInput,
    BreezeLabel,
  },

  data() {
    return {
      form: {
        email: "",
        processing: false,
        errors: [],
      },
    };
  },

  methods: {
    async submit() {
      this.form.processing = true;
      this.form.errors = [];

      try {
        await this.$axios.get("/sanctum/csrf-cookie");

        await this.$axios.post("/forgot-password", this.form);

        this.form.processing = false;
      } catch (e) {
        Object.keys(e.response.data.errors).forEach((key) => {
          Object.values(e.response.data.errors[key]).forEach((error) => {
            this.form.errors.push(error);
          });
        });
      }
    },
  },
};
</script>