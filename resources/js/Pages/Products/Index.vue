<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue'
import { Head, Link, router } from '@inertiajs/vue3'
import { ref } from 'vue'

const props = defineProps({
    products: Object,
    filters: Object,
    flash: Object,
})

const search = ref(props.filters?.search ?? '')

function cari() {
    router.get(route('products.index'), { search: search.value }, {
        preserveState: true,
        replace: true,
    })
}

function hapus(id) {
    if (confirm('Yakin ingin menghapus produk ini?')) {
        router.delete(route('products.destroy', id))
    }
}
</script>

<template>
    <Head title="Data Produk" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Data Produk
            </h2>
        </template>

        <div class="p-6">
            <div v-if="$page.props.flash?.success"
                 class="mb-4 rounded bg-green-100 p-3 text-green-800">
                {{ $page.props.flash.success }}
            </div>

            <div class="mb-4 flex flex-wrap items-center gap-3">
                <Link :href="route('products.create')"
                      class="rounded bg-blue-600 px-4 py-2 text-white">
                    + Tambah Produk
                </Link>

                <form @submit.prevent="cari" class="flex gap-2">
                    <input v-model="search"
                           type="text"
                           placeholder="Cari kode, nama, kategori"
                           class="rounded border-gray-300" />

                    <button class="rounded bg-gray-700 px-4 py-2 text-white">
                        Cari
                    </button>
                </form>
            </div>

            <div class="overflow-x-auto rounded bg-white shadow">
                <table class="w-full border-collapse text-left">
                    <thead class="bg-gray-100">
                        <tr>
                            <th class="p-3">Kode</th>
                            <th class="p-3">Nama Produk</th>
                            <th class="p-3">Kategori</th>
                            <th class="p-3">Harga</th>
                            <th class="p-3">Stok</th>
                            <th class="p-3">Aksi</th>
                        </tr>
                    </thead>

                    <tbody>
                        <tr v-for="product in products.data"
                            :key="product.id"
                            class="border-t">
                            <td class="p-3">{{ product.kode_produk }}</td>
                            <td class="p-3">{{ product.nama_produk }}</td>
                            <td class="p-3">{{ product.kategori }}</td>
                            <td class="p-3">
                                Rp {{ Number(product.harga).toLocaleString('id-ID') }}
                            </td>
                            <td class="p-3">{{ product.stok }}</td>
                            <td class="p-3">
                                <div class="flex gap-2">
                                    <Link :href="route('products.edit', product.id)"
                                          class="text-blue-600">
                                        Edit
                                    </Link>

                                    <button @click="hapus(product.id)"
                                            class="text-red-600">
                                        Hapus
                                    </button>
                                </div>
                            </td>
                        </tr>

                        <tr v-if="products.data.length === 0">
                            <td colspan="6" class="p-4 text-center text-gray-500">
                                Belum ada data produk.
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <div class="mt-4 flex flex-wrap gap-2">
                <template v-for="(link, index) in products.links" :key="index">
                    <Link v-if="link.url"
                          :href="link.url"
                          v-html="link.label"
                          class="rounded border px-3 py-1"
                          :class="{ 'bg-blue-600 text-white': link.active }" />
                </template>
            </div>
        </div>
    </AuthenticatedLayout>
</template>