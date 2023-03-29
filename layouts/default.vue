<template class="min-h-screen">
    <div class="flex">
        <div class="shadow-sm bg-[#1A1C22] text-white w-1/5 relative">
            <img src="~/assets/alkademi.png" class="mx-auto mt-10 mb-[120px]" height="200px" width="200px"/>
            <NavBar></NavBar>
            <img src="~/assets/mlbb.svg" alt="" width="200px" height="100px" class="absolute bottom-[20%] left-1/2 -translate-x-1/2">
        </div>
        <!-- Output content here -->
        <div class="w-4/5">
            <!-- <div class="h-20 bg-[#1A1C22] text-white flex p-4 justify-between">
                <div>
                    <h1 class="text-xl font-bold pt-2">Dashboard</h1>
                </div>
                <div>
                    <img src="~/assets/image.png" alt="">
                </div>
            </div> -->
            <div class="bg-gray-800 min-h-screen bg-[url('assets/bbg.jpg')] bg-cover">
                <slot />
            </div>
        </div>
    </div>
</template>

<script>
  
</script>

<style>
    .router-link-exact-active{
        color: #12b488
    }
    
</style>