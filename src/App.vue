<script setup>
    import { ref } from 'vue';
    import VPerfectSignature from 'v-perfect-signature';
    import { InformationCircleIcon } from '@heroicons/vue/solid';

    const signaturePad = ref();
    const strokeOptions = {
        size: 8,
        thinning: 0.5,
        smoothing: 0.5,
        streamline: 0.5,
        last: true,
    }

    const clear = () => {
        signaturePad.value?.clear()
    }

    const download = () => {
        if (signaturePad.value?.isEmpty()) {
            alert('Empty signature pad!')
            return
        }
        const link = document.createElement('a')
        link.download = 'signature.png'
        link.href = signaturePad.value?.toDataURL()
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
    }
</script>

<template>
    <main>
        <div class="max-w-5xl mx-auto py-6 sm:px-6 lg:px-8">
            <div class="rounded-md bg-blue-50 p-4">
                <div class="flex">
                    <div class="flex-shrink-0">
                        <InformationCircleIcon class="h-5 w-5 text-blue-400" aria-hidden="true" />
                    </div>
                    <div class="ml-3 flex-1 md:flex md:justify-between">
                        <p class="text-sm text-blue-700">We don't store image of your signature. You can check the code here in my <a href="https://github.com/eskiesirius/e-signature" class="link">github</a></p>
                    </div>
                </div>
            </div>
            <div class="px-4 py-6 sm:px-0">
                <div class="border-4 border-gray-200 h-64 rounded-lg">
                    <VPerfectSignature
                        ref="signaturePad"
                        :stroke-options="strokeOptions"
                    />
                </div>
                <div class="mt-10 text-center grid grid-cols-12 gap-4">
                    <button class="clear-btn col-span-12 md:col-span-6" @click="clear">
                        Clear and draw again
                    </button>
                    <button class="download-btn col-span-12 md:col-span-6" @click="download">
                        Download signature
                    </button>
                </div>
                <div class="mt-10">
                    Credits to <a href="https://github.com/wobsoriano/v-perfect-signature" class="link">wobsoriano</a> for this component.
                </div>
            </div>
        </div>
    </main>
</template>

<style>
.clear-btn {
    @apply px-4 py-2 font-medium tracking-wide text-gray-800 hover:text-white  capitalize transition-colors duration-200 transform rounded-md bg-white border border-gray-800 hover:bg-gray-700 focus:outline-none focus:text-white  focus:bg-gray-700;
}
.download-btn {
    @apply px-4 py-2 font-medium tracking-wide text-white hover:text-gray-800 capitalize transition-colors duration-200 transform rounded-md bg-gray-800 hover:bg-white hover:border-gray-800 hover:border  focus:outline-none;
}
.link {
    @apply underline text-blue-600 hover:text-blue-800 visited:text-purple-600
}
</style>
