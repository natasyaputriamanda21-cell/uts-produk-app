<script setup>
import { Link } from '@inertiajs/vue3';
</script>

<template>
    <aside class="w-64 bg-pink-500 text-white min-h-screen p-4 flex-shrink-0">
        <h2 class="text-lg font-bold mb-4">
            Toko Produk
        </h2>

        <nav class="space-y-2">
            <Link href="/dashboard" class="block hover:text-gray-300">
                Dashboard
            </Link>

            <Link href="/" class="block hover:text-gray-300">
                Beranda
            </Link>

            <Link href="/products" class="block hover:text-gray-300">
                Data Produk
            </Link>

            <Link href="/products/create" class="block hover:text-gray-300">
                Tambah Produk
            </Link>
        </nav>
    </aside>
</template>
