<template>
    <div class="home">
        <Chats/>
        <CreateChat/>
    </div>
</template>

<script>
import Chats from '@/components/Chat.vue'
import CreateChat from '@/components/Create.vue'

export default {
    name: 'ChatsView',
    components: {
        Chats,
        CreateChat
    }
}

</script>

<style scoped lang="less">

</style>