<script setup>
    import { Head, Link } from '@inertiajs/vue3';
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    defineOptions({
        layout: AuthenticatedLayout,
    })

    defineProps({
        products : Object,
    })
</script>
<template>
    <Head>
        <title>Product</title>
    </Head>
        <div>
            <h1 class="text-red-500">Products</h1>
            <Link :href="route('product.create')" class="p-1 rounded-full text-white bg-blue-500 hover:bg-blue-200">Add New Item</Link>
            <table class="table-auto">
                <thead>
                    <tr>
                        <td>No</td>
                        <td>Name</td>
                        <td>Price</td>
                        <td>Action</td>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in products" :key="product.id">
                        <td>{{ index + 1 }}</td>
                        <td>{{ product.name }}</td>
                        <td>{{ product.price }}</td>
                        <td>
                            <Link :href="route('product.edit', product.id)" class="p-1 rounded-full text-white bg-blue-500 hover:bg-blue-200">Edit</Link>
                            <Link :href="route('product.destroy', product.id)" as="button" method="DELETE" class="p-1 rounded-full text-white bg-red-500 hover:bg-red-200">Delete</Link>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
</template>
