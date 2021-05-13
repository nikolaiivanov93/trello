<template>
    <div class="group">
        <div class="group__wrapper">
            
            
            <div class="group__block">
                <div class="group__list-item">
                    <div class="group__name">{{ data.name }}</div>
                    <div class="group__text">{{ data.text }}</div>
                </div>
                <div class="group__info">
                    <div class="group__date">Date: <span class="date">{{ data.date }}</span></div>
                    <div class="group__priority">Priority: <span class="priority">{{ data.priority }}</span></div>
                </div>
                <button class="group__done" @click="done">Done</button>
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
            data: String,
            index: Number
        },
        data() {
            return {
                checkTask: false,
                taskInfo: {},
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
        watch: {
            task() {
                if(this.task.group !== null) {
                    this.checkTask = true;
                    this.taskInfo.name = this.task.name;
                }
            }
        },
        methods: {
            
            // addTask() {
            //     if(!this.newTask) {
            //         return;
            //     }

            //     this.task.push(this.newTask);
            //     this.newTask = '';
            //     this.saveTask();
            // },
            // removeTask() {
            //     this.task.splice(x, 1);
            //     this.saveTask();
            // },
            // saveTask() {
            //     const parsed = JSON.stringify(this.task);
            //     localStorage.setItem('task', parsed);
            // },
            done() {
                this.$emit('doneTask');
            }
        }
    }
</script>

<style>
.group {
    margin-bottom: 20px;
}
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
    background-color: rgba(0, 123, 255, 0.1);
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
.group__name {
    font-weight: 600;
    font-size: 22px;
    letter-spacing: 1px;
    width: 100%;
}
.group__text {
    font-size: 16px;
    font-weight: 400;
    margin-top: 7px;
    width: 100%;
}
.group__date, .group__priority {
    margin-top: 5px;
    font-weight: 700;
}
.name, .text, .date, .priority {
    font-weight: 400;
}
.group__done {
    width: 100px;
    height: 35px;
    border: 1px Solid #007bff;
    border-radius: 5px;
    background-color: rgba(0, 0, 0, 0);
}
</style>