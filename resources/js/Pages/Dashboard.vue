<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

</script>

<template>
    <Head title="Dashboard" />



    <AuthenticatedLayout>
        <div class="py-12 fade-in">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-blue-500 text-white">
    <h1 class="text-3xl font-bold mb-4">🐠 Welcome to the Fin-Tastic Fish Emporium! 🐟</h1>
    <p>Dive into a world of aquatic wonders at our store. For a limited time this December,</p>
    <p class="mb-4">enjoy exclusive discounts on our top-rated fish supplies!</p>
    <p>Explore our collection and provide the best care for your underwater friends. Don't miss out on the opportunity to enhance your aquatic experience.</p>
</div>
<br>
<hr class="border-t-2 border-blue-300 my-6">
<br>
<div class="p-6 bg-blue-500 text-white">
    <h1 class="text-3xl font-bold mb-4">Contact Us 📞</h1>
    <p class="mb-4">Have questions about our fish products or need assistance? Reach out to us!</p>
    <ul>
        <li><i class="fas fa-envelope mr-2"></i> Email: info@fintasticfishemporium.com</li>
        <li><i class="fas fa-phone mr-2"></i> Phone: +1 (123) 456-7890</li>
        <li><i class="fas fa-map-marker mr-2"></i> Address: 123 Ocean Avenue, Coral City, Atlantis</li>
    </ul>
</div>

                </div>
            </div>
        </div>
    </AuthenticatedLayout>





</template>
<style>

</style>
