<template>
    <h3>tasks:{{notyet}} tasks Done:{{already}} </h3>
    <button type="button" @click="deleteAllNodes"> tasks byebye </button>
    <button type="button" @click="deleteDoneNode"> done tasks byebye </button>
    <h4></h4>
    <button type="button" @click="this.value = 0; this.countListNumber();"> show all tasks  </button>
    <button type="button" @click="this.value = 1;  this.countListNumber();"> show done tasks </button>
    <button type="button" @click="this.value = 2;  this.countListNumber();"> show undone tasks </button>
    <h4></h4>>
    <button type="button" @click="create">add</button>
    <input v-model="message"> {{message}}
    <nodeInList v-for="column in decideWhatToShow" :time="column.time" :aaaa="column.isActive" :target="column.message" @fixToDoListName="fixToDoListName" @deleteCertainNode="deleteCertainNode" @changeStateOfIsactive="changeStateOfIsactive" :key="column.time"></nodeInList>
</template>


<script>
    import nodeInList from './components/nodeInList.vue'

    export default{
        name:'CreateButton',
        components: {
            nodeInList
        },
    data() {
        return{
            message : "temp",
            value: 0,
            notyet: 0,
            already: 0, 
            columns: []
        }
    },
    methods: {
        countListNumber() {
            this.notyet = 0;
            this.already = 0;
            if (this.columns.length == 0);
            else {
                var i = 0;
                for (; i < this.columns.length; i++) {
                    if (this.columns[i].isActive == false) this.notyet++;
                    else this.already++;

                    }
                }
            },
        changeStateOfIsactive(message) {//toggleActiveState
            var i = 0;
            for (; i < this.columns.length; i++) {
                if (this.columns[i].time == message) break;
            }
            var temp_active = !this.columns[i].isActive;
            console.log(temp_active);
            let arr = this.columns.slice();
            arr[i].isActive = temp_active;
            this.columns = arr;
            for (var y = 0; y < this.columns.length; y++) {
                this.columns[y].time += 1;
            }
            this.countListNumber();
        },
        deleteAllNodes() {
            this.columns.splice(0, this.columns.length);
            this.countListNumber();

        },
        deleteCertainNode(message) {
            console.log(message);
            var i = 0;
            for(; i <this.columns.length ; i++){
                if(message == this.columns[i].time) break;
            }
            this.columns.splice(i, 1);
            this.countListNumber();
            console.log(this.columns);
        },
        deleteDoneNode() {
            if (this.columns.length == 0); 
            else {
                var i = 0;
                for (; i < this.columns.length; i++) {
                    if (this.columns[i].isActive) this.columns.splice(i--, 1);

                }
            }
            this.countListNumber();
        },
        create() {
            var time = Date.now();
            this.columns.push({
                "message": this.message,
                "time": time,
                "isActive": false
            })
            this.countListNumber();
        },
        fixToDoListName(update) {
            var i = 0;
            for (; i < this.columns.length; i++) {
                if (this.columns[i].time == update[0].time) break;
            }
            this.columns[i].message = update[0].newmessage;
        }
    },
    computed: {
        decideWhatToShow () {
            if (this.value == 0) return this.columns;
            else if (this.value == 1) return this.columns.filter(i => i.isActive === true);
            else if (this.value == 2) return this.columns.filter(i => i.isActive === false);
            else return this.columns; 
        },
    }
        
}

</script>


<style>
</style>