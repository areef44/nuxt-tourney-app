<template>
  <div class="bg-[#1A1C22] h-20 text-2xl text-white">
    <h1 class="p-5 font-semibold">Team Dashboard</h1>
  </div>
  <div class="flex flex-col h-full">
    <!-- Table -->
    <div
      class="w-9/10 mx-6 my-12 bg-white shadow-lg rounded-sm border border-gray-200"
    >
      <header class="px-5 py-4 border-b border-gray-100">
        <div class="flex justify-center gap-5 py-4 pt-4">
        <h2 class="font-semibold text-gray-800">
          Daftar Team Peserta Turnamen
        </h2>
       <h2 class="font-semibold text-gray-800">
          Total Team = {{totalAll}}
        </h2>
       
            <button            
              class="bg-[#12b488] p-2 rounded-md text-white"
              @click="activate"
            >
            Lunas
            </button>
            <button
              class="bg-red-500  p-2 rounded-md text-white"
              @click="inactivate"
            >
            Belum Lunas
            </button>
             <button
              class="bg-violet-500  p-2 rounded-md text-white"
              @click="all"
            >
            ALL
            </button>
          </div>
      </header>
      <div class="p-3">
        <div class="overflow-x-auto">
          <table class="table-auto w-full">
            <thead
              class="text-xs font-semibold uppercase text-gray-400 bg-gray-50"
            >
              <tr>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-semibold text-left">No</div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-semibold text-left">Nama Team</div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-semibold text-left">Leader</div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-semibold text-center">Jumlah Anggota</div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-semibold text-center">Action</div>
                </th>
              </tr>
            </thead>
            <tbody class="text-sm divide-y divide-gray-100">
              <tr v-for="(team, index) in teamPage" :key="index">
                <td class="p-2 whitespace-nowrap">
                  <div class="font-medium text-gray-800">
                    {{ index + 1 + page * 8 }}
                  </div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="font-medium text-gray-800">{{ team.name }}</div>
                  </div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="text-left">{{ team.leader }}</div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="text-center font-medium text-green-500">
                    {{ team.totalMember }}
                  </div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="flex justify-center">
                    <NuxtLink :to="`/team/${team.id}`">
                      <p class="btn mr-1">Details</p>
                    </NuxtLink>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
          <div class="flex justify-center gap-5 py-4 pt-4">
            <button
            :class="{'bg-slate-400':(page <= 0),'bg-[#12b488]':(page > 0) }"
              class="bg-[#12b488] p-2 rounded-md text-white"
              @click="previousTeams"
              :disabled="page <= 0 ? true : false"
            >
            <Icon name="material-symbols:keyboard-double-arrow-left-rounded"/>
            </button>
            <button
              :class="{'bg-slate-400':(page >= totalPage-1),'bg-[#12b488]':(page < totalPage-1) }"
              class="  p-2 rounded-md text-white"
              @click="nextTeams"
              :disabled="page >= totalPage - 1 ? true : false"
            >
            <Icon name="material-symbols:keyboard-double-arrow-right"/>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const headers = {
  Authorization: "theMyth",
  "D-App-Authorization":
    "MjAyMy0wMy0yN1QyMToxNDo1Ny42MTNafGRldi5hbGthZGVtaS5pZHx2T1ZINnNkbXBOV2pSMjcxQ2M3cmR4czAxbHdIemZyMw==",
};
const res = await $fetch("https://services-dev.alkademi.id/v1/v1/team/list", {
  headers,
});
const Allteams = ref(res.data);
const totalAll = res.data.length
const slide = ref(0)
const teamPage = computed(()=> Allteams.value.slice(slide.value, slide.value + 8))
const totalTeam = computed(()=>Allteams.value.length);
const totalPage = computed(()=>Math.ceil(totalTeam.value / 8))
const page = ref(0);


function nextTeams() {    
  if (page.value < totalPage.value) {
    page.value++;
  }
  slide.value = page.value * 8;
}


function previousTeams() {
  if (page.value > 0) {
    page.value--;
  }
  slide.value = page.value * 8;
}

async function all(){
   const res = await $fetch("https://services-dev.alkademi.id/v1/v1/team/list", {
  headers,
});
const data = res.data
Allteams.value = data
slide.value = 0
page.value = 0

}

async function activate(){
  const res = await $fetch("https://services-dev.alkademi.id/v1/v1/team/list?status=active", {
  headers,
});
const data = res.data
Allteams.value = data
slide.value = 0
page.value = 0

}

async function inactivate(){
  const res = await $fetch("https://services-dev.alkademi.id/v1/v1/team/list?status=inactive", {
  headers,
});
const data = res.data
Allteams.value = data
slide.value = 0
page.value = 0
}
</script>

<style lang="scss" scoped>
</style>