<template>
    <div>
        <form @submit.prevent="submit">
            <div>
                <BreezeLabel for="email" value="Email" />
                <BreezeInput id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autofocus autocomplete="username" />
            </div>

            <div class="mt-4">
                <BreezeLabel for="password" value="Password" />
                <BreezeInput id="password" type="password" class="mt-1 block w-full" v-model="form.password" required autocomplete="current-password" />
            </div>

            <div class="block mt-4">
                <label class="flex items-center">
                    <BreezeCheckbox name="remember" :checked="form.remember" />
                    <span class="ml-2 text-sm text-gray-600">Remember me</span>
                </label>
            </div>

            <div class="flex items-center justify-end mt-4">
                <NuxtLink to="/forgot-password" class="underline text-sm text-gray-600 hover:text-gray-900">
                    Forgot your password?
                </NuxtLink>

                <BreezeButton class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Log in
                </BreezeButton>
            </div>
        </form>
    </div>
</template>

<script>
import BreezeButton from '@/components/button.vue'
import BreezeCheckbox from '@/components/checkbox.vue'
import BreezeInput from '@/components/input.vue'
import BreezeLabel from '@/components/label.vue'
export default {
    layout: 'guest',
    components: {
        BreezeButton,
        BreezeCheckbox,
        BreezeInput,
        BreezeLabel,
    },
    data() {
        return {
            form: {
                email: '',
                password: '',
                remember: false,
                processing: false
            }
        }
    },
    methods: {
        submit() {
            this.processing = true

            this.$auth.loginWith('laravelSanctum', {
                data: {
                    email: this.form.email,
                    password: this.form.password
                }
            }).then(() => {
                this.processing = false
            })
        }
    }
}
</script>