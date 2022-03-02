<template>
    <button type = "button" @click = "this.$emit('changeStateOfIsactive',newtime);"  >Ok</button>
    <span v-if="Active" class = "done">{{message}}</span>
    <span v-else >{{message}}</span>
    <button type="button" @click="this.$emit('deleteCertainNode',newtime);">delete</button>
    <input v-model="premessage">
    <button type = "button" @click = "fixToDoListName();"> fixToDoListName </button>
</template>

<script>
export default{
    name : 'nodeInList',
    props: ['target', 'aaaa', 'time'],
    data() {
        return {
            Active: this.aaaa,
            message: this.target,
            premessage: "none",
            newtime: this.time
        }
    },
    methods: {
        fixToDoListName() {
            var update = [];
            this.message = this.premessage;
            update.push({
                "time": this.newtime,
                "newmessage": this.premessage,
                "oldmessage": this.message,
            });
            this.$emit('fixToDoListName', update);
            
        }
    }
}
</script>


<style>
.done {
  color: red;
}
</style>