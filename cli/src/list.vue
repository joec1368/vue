<template>
    <h3>tasks:{{countUndoneTasks}} tasks Done:{{countDoneTasks}} </h3>
    <h4></h4>
    <button type="button" @click="deleteAllTasks" > tasks byebye </button>
    <button type="button" @click="deleteDoneNode"> done tasks byebye </button>
    <h4></h4>
    <buttonDecideElementToShow :value="this.value" @setValue = "setValue"></buttonDecideElementToShow>
    
    <button type="button" @click="create">add</button>
    <input v-model="message"> {{message}}

    <div v-for="element in decideWhatToShow" :key="element.time">
        <buttonToggleElementState  :time="element.time" :aaaa="element.isActive" :target="element.message" @toggleElementState="toggleElementState" :key="element.time"></buttonToggleElementState>
        <buttonDeleteCertainElement :time="element.time" @deleteCertainTask="deleteCertainTask" :key="element.time"></buttonDeleteCertainElement>>
        <buttonFixElementName :time="element.time" :target="element.message" @fixElementName="fixElementName" :key="element.time"></buttonFixElementName>
    </div>

</template>


<script>
    import buttonToggleElementState from './components/toggleElementState.vue'
    import buttonFixElementName from './components/fixElementName.vue'
    import buttonDeleteCertainElement from './components/deleteCertainElement.vue'
    import buttonDecideElementToShow from './components/decideElementToShow'

    export default{
        name:'listToDoList',
        components: {
            buttonToggleElementState,
            buttonDeleteCertainElement,
            buttonFixElementName,
            buttonDecideElementToShow
        },
    data() {
        return{
            message : "temp",
            show: "all",
            undoneTasks: 0,
            doneTasks: 0, 
            list: []
        }
    },
    methods: {
        setValue(valueShow){
            this.show = valueShow;
        },
        forceToUpdate(){
              for (var y = 0; y < this.list.length; y++) {
                this.list[y].time += 1;
            }
        },
        toggleElementState(message) {
            console.log("receive state");
            var i = 0;
            for (; i < this.list.length; i++) {
                if (this.list[i].time == message) break;
            }
            var temp_active = !this.list[i].isActive;
            console.log(temp_active);
            let arr = this.list.slice();
            arr[i].isActive = temp_active;
            this.list = arr;
            this.forceToUpdate();    
        },
        deleteAllTasks() {
            this.list = [];
        },
        deleteCertainTask(message) {
            console.log(message);
            var i = 0;
            for(; i <this.list.length ; i++){
                if(message == this.list[i].time) break;
            }
            this.list.splice(i, 1);
            console.log(this.list);
        },
        deleteDoneNode() {
            if (this.list.length == 0); 
            else {
                var i = 0;
                for (; i < this.list.length; i++) {
                    if (this.list[i].isActive) this.list.splice(i--, 1);

                }
            }
        },
        create() {
            var time = Date.now();
            this.list.push({
                "message": this.message,
                "time": time,
                "isActive": false
            })
        },
        fixElementName(update) {
            console.log("get");
            var i = 0;
            for (; i < this.list.length; i++) {
                if (this.list[i].time == update[0].time) break;
            }
            this.list[i].message = update[0].newmessage;
            this.forceToUpdate();           
        }
    },
    computed: {
        decideWhatToShow () {
            switch(this.show){
                case 'all':
                    return this.list;
                case 'done':
                    return this.list.filter(i => i.isActive === true);
                case 'undone':
                    return this.list.filter(i => i.isActive === false);
                default:
                    return this.list;
            }
        },
        countDoneTasks(){
           return this.list.filter(item => item.isActive).length;
        },
        countUndoneTasks(){
            return this.list.filter(item => !item.isActive).length;
        },
    }
        
}


</script>


<style>
</style>