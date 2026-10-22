<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link, useForm } from '@inertiajs/vue3'

const props = defineProps({
    product: Object,
})

const form = useForm({
    kode_produk: props.product.kode_produk,
    nama_produk: props.product.nama_produk,
    kategori: props.product.kategori,
    harga: props.product.harga,
    stok: props.product.stok,
})

function submit() {
    form.put(route('products.update', props.product.id))
}
</script>

<template>
    <Head title="Edit Produk" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold text-gray-800">
                Edit Produk
            </h2>
        </template>

        <div class="max-w-2xl p-6">
            <form @submit.prevent="submit" class="space-y-4 rounded bg-white p-6 shadow">
                <div>
                    <label class="mb-1 block">Kode Produk</label>
                    <input v-model="form.kode_produk"
                           class="w-full rounded border-gray-300" />
                    <p v-if="form.errors.kode_produk" class="text-sm text-red-600">
                        {{ form.errors.kode_produk }}
                    </p>
                </div>

                <div>
                    <label class="mb-1 block">Nama Produk</label>
                    <input v-model="form.nama_produk"
                           class="w-full rounded border-gray-300" />
                    <p v-if="form.errors.nama_produk" class="text-sm text-red-600">
                        {{ form.errors.nama_produk }}
                    </p>
                </div>

                <div>
                    <label class="mb-1 block">Kategori</label>
                    <input v-model="form.kategori"
                           class="w-full rounded border-gray-300" />
                    <p v-if="form.errors.kategori" class="text-sm text-red-600">
                        {{ form.errors.kategori }}
                    </p>
                </div>

                <div>
                    <label class="mb-1 block">Harga</label>
                    <input v-model="form.harga"
                           type="number" min="0" step="0.01"
                           class="w-full rounded border-gray-300" />
                    <p v-if="form.errors.harga" class="text-sm text-red-600">
                        {{ form.errors.harga }}
                    </p>
                </div>

                <div>
                    <label class="mb-1 block">Stok</label>
                    <input v-model="form.stok"
                           type="number" min="0" step="1"
                           class="w-full rounded border-gray-300" />
                    <p v-if="form.errors.stok" class="text-sm text-red-600">
                        {{ form.errors.stok }}
                    </p>
                </div>

                <div class="flex gap-3">
                    <button type="submit"
                            :disabled="form.processing"
                            class="rounded bg-blue-600 px-4 py-2 text-white">
                        Perbarui
                    </button>

                    <Link :href="route('products.index')"
                          class="rounded bg-gray-200 px-4 py-2">
                        Kembali
                    </Link>
                </div>
            </form>
        </div>
    </AuthenticatedLayout>
</template>