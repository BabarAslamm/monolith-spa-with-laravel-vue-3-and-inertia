<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';


defineProps({
    categories : {
        type : Array,
        required : true
    }
})

const form = useForm({
    name : '',
    brand : '',
    category_id : '',
    price : '',
    weight : '',
    description : '',
})

const store = () => {

    form.post(route('products.store'), {

        onSuccess : () => form.reset()

    })
}

</script>

<template>
    <Head title="Create Product" />

    <AuthenticatedLayout>
        <template #header>
            <div class="flex items-center justify-between">
                <h2 class="text-xl font-semibold leading-tight text-gray-800">
                    Create Product
                </h2>

                <!-- blue -->
                <Link :href="route('products.index')" class="px-3 py-2.5 text-sm font-medium text-center text-white bg-blue-700 rounded-md hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300">Manage Products</Link>
                
            </div>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="flex items-center justify-center">
                    <div class="relative w-full max-w-2xl max-h-full">
                        <form class="relative bg-white rounded-lg shadow" @submit.prevent="store">
                            <div class="p-6 space-y-6">
                                <div class="grid grid-cols-6 gap-6">
                                    <div class="col-span-6 sm:col-span-6">
                                        <label
                                            for="name"
                                            class="block mb-2 text-sm font-medium text-gray-900"
                                            :class="form.errors.name ? 'text-red-700' : 'text-gray-900'">
                                            Product name
                                        </label>

                                        <input
                                            type="text"
                                            v-model="form.name"
                                            name="name" id="name"
                                            :class="form.errors.name ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'"

                                            >
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.name">{{ form.errors.name }}</div>

                                    </div>
                                    <div class="col-span-6 sm:col-span-3">
                                        <label for="brand" class="block mb-2 text-sm font-medium text-gray-900 ">Brand</label>
                                        <input type="text" v-model="form.brand" name="brand" id="brand" :class="form.errors.brand ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'">
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.brand">{{ form.errors.brand }}</div>
                                    </div>
                                    <div class="col-span-6 sm:col-span-3">
                                        <label for="category_id" class="block mb-2 text-sm font-medium text-gray-900 ">Category</label>
                                        <select v-model="form.category_id" name="category_id" id="category_id" :class="form.errors.category_id ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'">
                                            <option value="">Select a category</option>
                                            <option v-for="category in categories" :key="category.id" :value="category.id">{{ category.name }}</option>
                                            <option value="">Category 3</option>
                                        </select>
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.category_id">{{ form.errors.category_id }}</div>
                                    </div>
                                    <div class="col-span-6 sm:col-span-3">
                                        <label for="price" class="block mb-2 text-sm font-medium text-gray-900 ">Price</label>
                                        <input type="number" v-model="form.price" name="price" id="price" :class="form.errors.price ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'">
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.price">{{ form.errors.price }}</div>
                                    </div>
                                    <div class="col-span-6 sm:col-span-3">
                                        <label for="weight" class="block mb-2 text-sm font-medium text-gray-900 ">Weight</label>
                                        <input type="number" v-model="form.weight" name="weight" id="weight" :class="form.errors.weight ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'">
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.weight">{{ form.errors.weight }}</div>
                                    </div>
                                    <div class="col-span-6 sm:col-span-6">
                                        <label for="description" class="block mb-2 text-sm font-medium text-gray-900 ">Description</label>
                                        <textarea v-model="form.description" name="description" id="description" :class="form.errors.description ? 'shadow-sm bg-red-50 border border-red-500 text-red-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5' : 'shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-600 focus:border-blue-600 block w-full p-2.5'" rows="3"></textarea>
                                        <div class="font-sm text-red-500 mt-2" v-if="form.errors.description">{{ form.errors.description }}</div>
                                    </div>
                                    <div class="col-span-6 sm:col-span-6 space-x-2">
                                        <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center">Save</button>
                                        <button type="button" class="text-gray-900 bg-white border border-gray-300 focus:outline-none hover:bg-gray-100 focus:ring-4 focus:ring-gray-200 font-medium rounded-lg text-sm px-5 py-2.5">Cancel</button>
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
