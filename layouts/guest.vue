<template>
    <div class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100">
        <div>
            <NuxtLink to="/">
                <ApplicationLogo class="w-20 h-20 fill-current text-gray-500" />
            </NuxtLink>
        </div>

        <div class="w-full sm:max-w-md mt-6 px-6 py-4 bg-white shadow-md overflow-hidden sm:rounded-lg">
            <Nuxt />
        </div>
    </div>
</template>

<script>
export default {
    middleware: 'guest'
}
</script>
