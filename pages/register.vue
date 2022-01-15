<template>
    <div>
        <form @submit.prevent="submit">
            <div>
                <BreezeLabel for="name" value="Name" />
                <BreezeInput id="name" type="text" class="input mt-1 block w-full" v-model="form.name" required autofocus autocomplete="name" />
            </div>

            <div class="mt-4">
                <BreezeLabel for="email" value="Email" />
                <BreezeInput id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autocomplete="username" />
            </div>

            <div class="mt-4">
                <BreezeLabel for="password" value="Password" />
                <BreezeInput id="password" type="password" class="mt-1 block w-full" v-model="form.password" required autocomplete="new-password" />
            </div>

            <div class="mt-4">
                <BreezeLabel for="password_confirmation" value="Confirm Password" />
                <BreezeInput id="password_confirmation" type="password" class="mt-1 block w-full" v-model="form.password_confirmation" required autocomplete="new-password" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <NuxtLink to="/login" class="underline text-sm text-gray-600 hover:text-gray-900">
                    Already registered?
                </NuxtLink>

                <BreezeButton class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Register
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
                name: '',
                email: '',
                password: '',
                password_confirmation: '',
                terms: false,
                processing: false
            }
        }
    },
    methods: {
        submit() {
            this.processing = true

            this.$axios.get('sanctum/csrf-cookie').then(() => {
                this.$axios.$post('register', this.form).then(() => {
                    this.$auth.loginWith('laravelSanctum', {
                        data: this.form
                    }).then(() => {
                        this.processing = false
                    })
                })
            })
        }
    }
}
</script>
