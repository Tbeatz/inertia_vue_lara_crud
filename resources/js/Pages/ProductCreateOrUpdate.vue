<script setup>
    import { Head, Link, router } from '@inertiajs/vue3';
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import { ref } from 'vue';

    defineOptions({
        layout : AuthenticatedLayout,
    });

    const props = defineProps({
        errors : Object,
        status : String,
        product : Object,
    });

    const form = ref({
        name : props.product ? props.product.name : '',
        price: props.product ? props.product.price : '',
    });

    // function submit() {
    //     console.log('test');
    //     router.post(props.status == 'create' ? route('product.store', form) : route('product.update', form))
    // }

</script>
<template>
    <Head><title>Create</title></Head>
    <h1>This is Product {{ props.status == 'edit' ? 'Edit' : 'Create' }} page</h1>
    <!-- <form method="POST" @submit.prevent="submit"> -->
    <form>
        <input type="text" v-model="form.name">
        <div v-if="errors.name">{{ errors.name }}</div>
        <input type="text" v-model="form.price">
        <div v-if="errors.price">{{ errors.price }}</div>
        <Link
            as="button"
            :data="form"
            :method="props.status == 'create' ? 'POST' : 'PATCH'"
            type="button"
            :href="props.status == 'create' ? route('product.store') : route('product.update', props.product.id)"
            class="text-white bg-gray-900 border-b-orange-600 rounded-full p-3 hover:bg-gray-600"
        >
            {{ props.status == 'create' ? 'Save' : 'Update'}}
        </Link>
    </form>
</template>
