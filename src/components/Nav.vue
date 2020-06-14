<template>
    <header class="bg-teal-900 border-b-2 border-red-400 shadow-md">
        <div class="container mx-auto px-6 py-4 md:flex items-center justify-between">
            <div class="flex items-center justify-between">
                <div>
                    <h1 class="text-2xl font-semibold text-teal-200">Shop</h1>
                </div>

                <div class="md:hidden">
                    <button @click="isOpen = !isOpen" type="button" class="text-gray-500 hover:text-white focus:text-white focus:outline-none">
                        <svg class="h-6 w-6 fill-current" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                            <path v-if="isOpen" d="M6 18L18 6M6 6l12 12"></path>
                            <path v-if="!isOpen" d="M4 6h16M4 12h16M4 18h16"></path>
                        </svg>
                    </button>
                </div>
            </div>

            <div :class="isOpen ? 'block' : 'hidden'" class="md:flex -mx-2">
                <a href="#" class="block px-2 py-1 text-white font-semibold rounded hover:bg-teal-800">Product</a>
                <a href="#" class="mt-1 block px-2 py-1 text-white font-semibold rounded hover:bg-teal-800 md:mt-0 md:ml-2">Cart</a>
                <a href="#" class="mt-1 block px-2 py-1 text-white font-semibold rounded hover:bg-teal-800 md:mt-0 md:ml-2">Category</a>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name:'Nav',
    data() {
        return {
            isOpen:false,
        }
    },
}
</script>