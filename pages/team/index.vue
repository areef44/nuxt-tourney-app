<template>
  <div class="bg-[#1A1C22] h-20 text-2xl text-white">
    <h1 class="p-5 font-semibold">Team Dashboard</h1>
  </div>
  <div class="flex flex-col h-full">
    <!-- Table -->
    <div class="w-9/10 mx-6 my-2 bg-white shadow-lg rounded-sm border border-gray-200">
      <header class="px-5 py-1 border-b border-gray-100">
        <div class=" gap-5 py-1 pt-4">
          <div class="flex justify-between">
            <h2 class="font-semibold text-gray-800">
              Daftar Team Peserta Turnamen
            </h2>
           <h2 class="font-semibold text-gray-800">
              Total Team = {{totalAll}}
            </h2>
          </div>          
          <div class="text-xs flex justify-end py-2">
            <h1 class="font-semibold text-md">Tampilkan : </h1>
            <select data-te-select-init data-te-select-size="lg" name="" id="" @change="teamsSelect($event)">
          <option value="all" selected>Semua</option>
          <option value="active">Sudah Bayar</option>
          <option value="inactive">Belum Bayar</option>
        </select>
           
          </div>
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
                    <div class="font-semibold text-gray-800">{{ team.name }}</div>
                  </div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="text-left">{{ team.leader }}</div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="text-center font-semibold text-red-500">
                    {{ team.totalMember }}
                  </div>
                </td>
                <td class="p-2 whitespace-nowrap">
                  <div class="flex justify-center">
                    <NuxtLink :to="`/team/${team.id}`">
                      <p class="btn hover:bg-slate-500 mr-1">Details</p>
                    </NuxtLink>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
          <div class="flex justify-center gap-5 py-4 pt-4">
            <button
            :class="{'bg-slate-400':(page <= 0),'bg-[#12b488]':(page > 0) }"
              class="bg-[#12b488] p-2 rounded-md text-white hover:bg-slate-500"
              @click="previousTeams"
              :disabled="page <= 0 ? true : false"
            >
            <Icon name="material-symbols:keyboard-double-arrow-left-rounded"/>
            </button>
            <button
              :class="{'bg-slate-400':(page >= totalPage-1),'bg-[#12b488]':(page < totalPage-1) }"
              class="  p-2 rounded-md text-white hover:bg-slate-500"
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
const baseUrl = "https://services.alkademi.id/v1/v1/team/"
const author = "2d317a6b0048b438d219f8ffc8c5b927322415"
const token = "MjAyMy0wNC0wMVQxNDowMjozNS40MTZafGZ1bi5hbGthZGVtaS5pZHx2T1ZINnNkbXBOV2pSMjcxQ2M3cmR4czAxbHdIemZyMw=="
const headers = {
  Authorization: author,
  "D-App-Authorization":
    token,
};
const res = await $fetch(`${baseUrl}list`, {
  headers,
});
console.log(res)
const Allteams = ref(res.data);
const totalAll = res.data.length
const slide = ref(0)
const teamPage = computed(()=> Allteams.value.slice(slide.value, slide.value + 8))
const totalTeam = computed(()=>Allteams.value.length);
const totalPage = computed(()=>Math.ceil(totalTeam.value / 8))
const page = ref(0);

function teamsSelect(e){
  switch (e.target.value) {
      case "all":
      all();
      break;
      case "active":
      activate();
      break;
      case "inactive":
      inactivate();
      break;
  
    default:
      all();
      break;
  }
}

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
   const res = await $fetch(`${baseUrl}list`, {
  headers,
});
const data = res.data
Allteams.value = data
slide.value = 0
page.value = 0

}

async function activate(){
  const res = await $fetch(`${baseUrl}list?status=active`, {
  headers,
});
const data = res.data
Allteams.value = data
slide.value = 0
page.value = 0

}

async function inactivate(){
  const res = await $fetch(`${baseUrl}list?status=inactive`, {
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