<template>
    <div>
        <p>detail team {{ id }}</p>
        <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Dicta placeat recusandae delectus animi neque cumque doloremque nemo iste quasi soluta cum vero itaque provident deserunt velit, exercitationem et totam ipsa?</p>
    </div>
</template>

<script setup>
    const { id } = useRoute().params
</script>

<style lang="scss" scoped>

</style>