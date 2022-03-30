<template>
    <br/>
    <button type = "button" @click = "this.$emit('toggleTaskState',index);"  >Ok</button>
    <span v-if="active" class = "done">{{messageInComponent}}</span>
    <span v-else >{{messageInComponent}}</span>

    <button type="button" @click="this.$emit('deleteCertainTask',time);">delete</button>
    
    <input v-model="messageNewName">
    <button type = "button" @click = "fixTaskName();"> fixTaskName </button>
</template>

<script>

export default{
    name : 'tasksComponents',
    props: ['message', 'active','index','time'],
    data() {
        return {
            Active: this.active,
            messageInComponent: this.message,
            messageNewName : 'none'
        }
    },
    methods: {
        fixTaskName() {
            var updateMessagePack = [];
            updateMessagePack.push({
                "message": this.messageNewName,
                "time": this.time
            });
            this.$forceUpdate();
            this.$emit('fixTaskName', updateMessagePack);
            
        }
    }
}
</script>
<style>
.done {
  color: red;
}
</style>