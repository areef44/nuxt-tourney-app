<template>
  <div>
    <div class="bg-[#1A1C22] h-full">
      <div class="flex justify-between">
        <h1 class="text-white font-bold text-2xl py-2 ml-4">
          {{ teamDetails.name }} E-Sports Members
        </h1>        
        <NuxtLink to="/team">
          <p class="btn-del mr-4 my-2 font-bold">Kembali</p>
        </NuxtLink>
      </div>
    </div>

       <div class="text-white font-bold text-xl bg-[#1A1C22] pl-4">
          <div class="mr-4">
              <h1>Leader : {{ teamDetails.leader.name }}</h1>
          </div>
          <div class="flex justify-between mt-2">
              <h1 class="mb-2">Status Pembayaran : {{ statusPembayaran }}</h1>
              <button @click="onToggle" class="btn-edit mr-4 mb-2" v-if="statusPembayaran !== 'Lunas' ">Konfirmasi Pembayaran</button>
          </div>
        </div>

    <div class="grid grid-cols-3 gap-1">
      <div
        class="p-8 bg-white shadow mt-8 mx-4 rounded-md"
        v-for="(member, index) in teamMembers"
        :key="index"
      >
        <div class="text-center text-gray-800">
          <img src="~/assets/medal.png" alt="" width="25px" class="center">
          <h1 class="text-2xl font-semibold my-2">{{ member.name }}</h1>
          <p class="">
            <Icon name="ic:baseline-email" class="mr-1 my-1" />{{
              member.email
            }}
          </p>
          <p class="">
            <Icon name="ic:baseline-phone-android" class="mr-1 my-1" />{{
              member.phone
            }}
          </p>
          <p class="">
            <Icon name="ic:baseline-school" class="mr-1 my-1" />{{
               (/:"(.*)"/.exec(member.custom_fields)[1])
            }}
          </p>
          <p class="font-light">
            <Icon name="ic:baseline-location-city" class="mr-1 my-1" />{{
              member.address
            }}
          </p>
        </div>
      </div>
    </div>
    <!-- modal -->
    <transition name="fade">
      <div v-if="isModalVisible">
        <div
          @click="onToggle"
          class="absolute bg-black opacity-70 inset-0 z-0"
        ></div>
        <div
          class="bottom-[40%] left-[40%] w-full max-w-lg p-3 absolute mx-auto my-auto rounded-xl shadow-lg bg-white"
        >
          <div>
            <div class="text-center p-3 flex-auto justify-center leading-6">
              <h2 class="text-2xl font-bold py-4">Konfirmasi Pembayaran</h2>
              <p class="text-md text-gray-500 px-8">
                Apakah Anda Ingin Mengkonfirmasi Pembayaran?
              </p>
            </div>
            <div class="p-3 mt-2 text-center space-x-4 md:block">
              <button class="btn-save" @click="onToggle() ; activate()">Konfirmasi</button>
              <button @click="onToggle" class="btn-del">Kembali</button>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup>
const { id } = useRoute().params;
const headers = {
  Authorization: "theMyth",
  "D-App-Authorization":
    "MjAyMy0wMy0yN1QyMToxNDo1Ny42MTNafGRldi5hbGthZGVtaS5pZHx2T1ZINnNkbXBOV2pSMjcxQ2M3cmR4czAxbHdIemZyMw==",
};
const res = await $fetch(
  `https://services-dev.alkademi.id/v1/v1/team/detail?id=${id}`,
  { headers }
);
const teamDetails = reactive(res.data);
const teamMembers = teamDetails.members;
const statusPembayaran = computed(() => teamDetails.status === 0 ? "Belum Lunas" : "Lunas");
const isOpen = ref(false);
const isModalVisible = computed(() => isOpen.value);
function onToggle() {
  isOpen.value = !isOpen.value;
}

async function activate(){
  await $fetch(
  `https://services-dev.alkademi.id/v1/v1/team/update/activate?id=${id}`,
  { headers }
);
const res =  await $fetch(
  `https://services-dev.alkademi.id/v1/v1/team/detail?id=${id}`,
  { headers }
)
const newData = res.data
teamDetails.status = newData.status 
}

</script>

<style scoped>

.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

</style>