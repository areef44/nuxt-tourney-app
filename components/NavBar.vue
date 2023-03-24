<template>
            <nav>
                <ul class="text-xl ml-16 font-semibold">
                    <div class="flex my-11">
                        <div class="mr-4">
                            <li><Icon name="ic:round-house"/></li>
                        </div>
                        <div class="p-[2px]">
                            <li><NuxtLink to="/">Dashboard</NuxtLink></li>
                        </div>
                    </div>
                    <div class="flex my-11">
                        <div class="mr-4">
                            <li><Icon name="mdi:account-group"/></li>
                        </div>
                        <div class="p-[3px]">
                            <li><NuxtLink to="/team">Team</NuxtLink></li>
                        </div>
                    </div>
                    <div class="flex my-11">
                        <div class="mr-4">
                            <li><Icon name="ph:currency-circle-dollar-bold"/></li>
                        </div>
                        <div class="p-[3px]">
                            <li><NuxtLink to="/pembayaran">Pembayaran</NuxtLink></li>
                        </div>
                    </div>
                    <div class="flex my-11">
                        <div class="mr-4">
                            <li><Icon name="mdi:document"/></li>
                        </div>
                        <div class="p-[3px]">
                            <li><NuxtLink to="/laporan">Laporan</NuxtLink></li>
                        </div>
                    </div>
                    <div class="flex my-11">
                        <div class="mr-4">
                            <li><Icon name="mdi:logout"/></li>
                        </div>
                        <div class="p-[3px]">
                            <li><NuxtLink to="/laporan">Log Out</NuxtLink></li>
                        </div>
                    </div>
                </ul>
            </nav>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>