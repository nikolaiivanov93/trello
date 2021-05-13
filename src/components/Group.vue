<template>
    <div>
        <div class="group__wrapper">
            <div class="group__opt">
                <div v-for="option in options" 
                :key="option.group" 
                class="group__options"
                
                >
                {{ option.group }}</div>
            </div>
            
            <div class="group__block">
                <div class="group__list-item">
                    <div class="group__name">Task name: <span class="name">{{ task.name }}</span></div>
                    <div class="group__text">Note text: <span class="text">{{ task.text }}</span></div>
                </div>
                <div class="group__info">
                    <div class="group__date">Date: <span class="date">{{ task.date }}</span></div>
                    <div class="group__priority">Priority: <span class="priority">{{ task.priority }}</span></div>
                </div>
                <button @click="done">Done</button>
            </div>
        </div>
    </div>
</template>
    
<script>
    export default {
        name: 'group',
        props: {
            task: Object,
            newTask: null,
        },
        data() {
            return {
                options: [
                    {group: "Work"},
                    {group: "Home"},
                    {group: "Sport"},
                    {group: "Buy"}
                ],
            }
        },
        mounted() {
            if (localStorage.getItem('task')) {
            try {
                this.task = JSON.parse(localStorage.getItem('task'));
            } catch(e) {
                localStorage.removeItem('task');
            }
            }
        },
        methods: {
            addTask() {
                if(!this.newTask) {
                    return;
                }

                this.task.push(this.newTask);
                this.newTask = '';
                this.saveTask();
            },
            removeTask() {
                this.task.splice(x, 1);
                this.saveTask();
            },
            saveTask() {
                const parsed = JSON.stringify(this.task);
                localStorage.setItem('task', parsed);
            },
            done() {
                console.log(this.task)
            }
        }
    }
</script>

<style>
.group__wrapper {
    width: 400px;
    height: 100%;
    margin-left: 40px;
   /*  border: 1px Solid #000; */
}
.group__block {
    width: 100%;
    min-height: 50px;
    padding-bottom: 20px;
    border: 1px Solid rgb(247, 152, 11);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.group__item {
    font-size: 22px;
    font-weight: 600;
}
.group__list-item {
    width: 100%;
    padding: 0 10px;
}
.group__info {
    width: 100%;
    padding: 0 10px;
    display: flex;
    justify-content: space-between;
}
.group__opt {
    display: flex;
    justify-content: space-between;
    padding-bottom: 20px;
}
.group__options {
    font-size: 22px;
    font-weight: 700;
}
.group__name, .group__text, .group__date, .group__priority {
    font-weight: 700;
}
.name, .text, .date, .priority {
    font-weight: 400;
}
</style>