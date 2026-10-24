
<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { useForm, Head } from '@inertiajs/vue3';

const form = useForm({
    kode_produk: '',
    nama_produk: '',
    kategori: '',
    harga: '',
    stok: 0,
});

function submit() {
    form.post(route('products.store'));
}
</script>

<template>
    <Head title="Tambah Produk" />

    <AuthenticatedLayout>
        <div class="p-6">
            <h1 class="mb-6 text-xl font-bold">
                Tambah Produk
            </h1>

            <form @submit.prevent="submit">
                <div class="flex flex-nowrap items-end gap-3 overflow-x-auto pb-3">

                    <div class="flex min-w-[130px] flex-col">
                        <label class="mb-2">Kode Produk</label>

                        <input
                            v-model="form.kode_produk"
                            type="text"
                            class="w-full rounded border border-gray-300 px-3 py-2"
                            required
                        />
                        <span
                            v-if="form.errors.kode_produk"
                            class="text-sm text-red-500"
                        >
                            {{ form.errors.kode_produk }}
                        </span>
                    </div>

                    <div class="flex min-w-[150px] flex-col">
                        <label class="mb-2">Nama Produk</label>

                        <input
                            v-model="form.nama_produk"
                            type="text"
                            class="w-full rounded border border-gray-300 px-3 py-2"
                            required
                        />
                        <span
                            v-if="form.errors.nama_produk"
                            class="text-sm text-red-500"
                        >
                            {{ form.errors.nama_produk }}
                        </span>
                    </div>

                    <div class="flex min-w-[130px] flex-col">
                        <label class="mb-2">Kategori</label>

                        <input
                            v-model="form.kategori"
                            type="text"
                            class="w-full rounded border border-gray-300 px-3 py-2"
                            required
                        />
                        <span
                            v-if="form.errors.kategori"
                            class="text-sm text-red-500"
                        >
                            {{ form.errors.kategori }}
                        </span>
                    </div>

                    <div class="flex min-w-[130px] flex-col">
                        <label class="mb-2">Harga</label>

                        <input
                            v-model="form.harga"
                            type="number"
                            min="0"
                            class="w-full rounded border border-gray-300 px-3 py-2"
                            required
                        />
                        <span
                            v-if="form.errors.harga"
                            class="text-sm text-red-500"
                        >
                            {{ form.errors.harga }}
                        </span>
                    </div>

                    <div class="flex min-w-[90px] flex-col">
                        <label class="mb-2">Stok</label>

                        <input
                            v-model="form.stok"
                            type="number"
                            min="0"
                            class="w-full rounded border border-gray-300 px-3 py-2"
                            required
                        />
                        <span
                            v-if="form.errors.stok"
                            class="text-sm text-red-500"
                        >
                            {{ form.errors.stok }}
                        </span>
                    </div>

                    <button
                        type="submit"
                        :disabled="form.processing"
                        class="whitespace-nowrap rounded bg-blue-600 px-4 py-2 text-white hover:bg-blue-700 disabled:opacity-50"
                    >
                        {{ form.processing ? 'Menyimpan...' : 'Simpan' }}
                    </button>

                </div>
            </form>
        </div>
    </AuthenticatedLayout>
</template>
