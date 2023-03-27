<template>

    <div class="flex flex-col h-full">
        <!-- Table -->
        <div class="w-9/10 mx-6 my-12 bg-white shadow-lg rounded-sm border border-gray-200">
            <header class="px-5 py-4 border-b border-gray-100">
                <h2 class="font-semibold text-gray-800">Daftar Team Peserta Turnamen</h2>
            </header>
            <div class="p-3">
                <div class="overflow-x-auto">
                    <table class="table-auto w-full">
                        <thead class="text-xs font-semibold uppercase text-gray-400 bg-gray-50">
                            <tr>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">No</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">Nama Team</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">Email</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">Jumlah Anggota</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-center">Alamat</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-center">Action</div>
                                </th>
                            </tr>
                        </thead>
                        <tbody class="text-sm divide-y divide-gray-100">
                            <tr>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="font-medium text-gray-800">1</div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="flex items-center">
                                        <div class="w-10 h-10 flex-shrink-0 mr-2 sm:mr-3"><img class="rounded-full" src="https://raw.githubusercontent.com/cruip/vuejs-admin-dashboard-template/main/src/images/user-36-05.jpg" width="40" height="40" alt="Alex Shatov"></div>
                                        <div class="font-medium text-gray-800">Alex Shatov</div>
                                    </div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="text-left">alexshatov@gmail.com</div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="text-left font-medium text-green-500">$2,890.66</div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="text-lg text-center">??</div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="flex justify-center">
                                        <NuxtLink :to="`/team/{id}`">
                                            <p class="btn mr-1">Details</p>
                                        </NuxtLink>
                                        <div id="app">
                                            <div class="flex flex-col items-center justify-center min-h-full relative">
                                                <button @click="onToggle"
                                                class="btn-edit">
                                                Confirm
                                                </button>
                                            </div>
                                            <transition name="fade">
                                                <div v-if="isModalVisible">
                                                <div @click="onToggle" class="absolute bg-black opacity-70 inset-0 z-0">
                                                </div>
                                                <div class="bottom-[40%] left-[40%] w-full max-w-lg p-3 absolute mx-auto my-auto rounded-xl shadow-lg bg-white">
                                                    <div>
                                                    <div class="text-center p-3 flex-auto justify-center leading-6">
                                                        <h2 class="text-2xl font-bold py-4">Konfirmasi Pembayaran</h2>
                                                        <p class="text-md text-gray-500 px-8">
                                                            Apakah Anda Ingin Mengkonfirmasi Pembayaran?
                                                        </p>
                                                    </div>
                                                    <div class="p-3 mt-2 text-center space-x-4 md:block">
                                                        <button class="btn-save">
                                                        Simpan
                                                        </button>
                                                        <button @click="onToggle" class="btn-del">
                                                        Kembali
                                                        </button>
                                                    </div>
                                                    </div>
                                                </div>
                                                </div>
                                            </transition>
                                        </div>
                                    </div>
                                </td>
                            </tr>                                                                 
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    
</template>

<script>
    export default {
    data() {
      return {
        isOpen: false
      };
    },
  
    computed: {
      isModalVisible() {
        return this.isOpen;
      }
    },
  
    methods: {
      onToggle() {
        this.isOpen = !this.isOpen;
      }
    }
  };
</script>

<style lang="scss" scoped>

</style>