<template>
    <div>
        <div class="mb-4 text-sm text-gray-600">
            Forgot your password? No problem. Just let us know your email address and we will email you a password reset link that will allow you to choose a new one.
        </div>

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <BreezeLabel for="email" value="Email" />
                <BreezeInput id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autofocus autocomplete="username" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <BreezeButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Email Password Reset Link
                </BreezeButton>
            </div>
        </form>
    </div>
</template>

<script>
import BreezeButton from '@/components/button.vue'
import BreezeInput from '@/components/input.vue'
import BreezeLabel from '@/components/label.vue'
export default {
    layout: 'guest',
    components: {
        BreezeButton,
        BreezeInput,
        BreezeLabel,
    },
    data() {
        return {
            form: {
                email: '',
                processing: false
            }
        }
    },
    methods: {
        submit() {
            this.processing = true

            this.$axios.get('sanctum/csrf-cookie').then(() => {
                this.$axios.post('/forgot-password', this.form).then(() => {
                    this.processing = false
                })
            })
        }
    }
}
</script>