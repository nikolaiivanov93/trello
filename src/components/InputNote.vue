<template>
    <div>
        <div class="note__wrapper">
            <div class="note__input">
                <span class="note__name">Task name: </span><input v-model="name"/>
                <span class="note__text">Note text: </span><textarea v-model="text" class="note__txt"/>
            </div>
            <div class="note__priority">Priority</div>
            <div class="note__priority_radio">
                <b-form-radio-group
                    id="btn-radios-2"
                    v-model="selectedPriority"
                    :options="optionsPriority"
                    :aria-describedby="ariaDescribedby"
                    button-variant="outline-primary"
                    size="lg"
                    name="radio-btn-outline"
                    buttons
                ></b-form-radio-group>
            </div>
            <div class="note__group">Group</div>
            <div class="note__group_radio">
                <b-form-radio-group
                    id="btn-radios-2"
                    v-model="selectedGroup"
                    :options="optionsGroup"
                    :aria-describedby="ariaDescribedby"
                    button-variant="outline-primary"
                    size="lg"
                    name="radio-btn-outline"
                    buttons
                ></b-form-radio-group>
            </div>
            <div class="note__date">Date</div>
            <div>
                <b-calendar v-model="value" :min="min" :max="max" locale="en"></b-calendar>
            </div>
            <div>
                <button @click="setTask" class="note__btn">Add</button>
                <button class="note__btn">Clear</button>
            </div>
        </div>
    </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

export default {
    name: 'InputNote',
    data() {
        const now = new Date()
        const today = new Date(now.getFullYear(), now.getMonth(), now.getDate())
        // 15th two months prior
        const minDate = new Date(today)
        minDate.setMonth(minDate.getMonth() - 2)
        minDate.setDate(15)
        // 15th in two months
        const maxDate = new Date(today)
        maxDate.setMonth(maxDate.getMonth() + 2)
        maxDate.setDate(15)
        return {
            selectedPriority: [], // Must be an array reference!
            optionsPriority: [
                { text: 'Important', value: 'Important' },
                { text: 'Normal', value: 'Normal' },
                { text: 'Wait', value: 'Wait' },
            ],
            selectedGroup: [],
            optionsGroup: [
                { text: 'Work', value: 'Work' },
                { text: 'Home', value: 'Home' },
                { text: 'Sport', value: 'Sport' },
                { text: 'Buy', value: 'Buy' },
            ],
            value: '',
            min: minDate,
            max: maxDate,
            task: [],
            name: "",
            text: "",
        }
    },
    methods: {
        setTask() {
            // this.task.priority = this.selectedPriority;
            // this.task.group = this.selectedGroup;
            // this.task.date = this.value;
            // this.task.name = this.name;
            // this.task.text = this.text;
            // this.task.push(info);
            this.task.push({
                priority: this.selectedPriority,
                group: this.selectedGroup,
                date: this.value,
                name: this.name,
                text: this.text});
            console.log('tasktask',this.task)
            this.$emit('setGroup', this.task);
            this.name = '';
            this.text = '';
            this.selectedPriority = [];
            this.selectedGroup = [];
            this.value = '';
            // this.$emit('setOptions', this.optionsGroup);
            console.log(this.task)
            // this.$emit('setGroup', this.selectedGroup);
        }
    }
}

</script>

<style>
.note__name {
    margin-bottom: 10px;
    font-size: 22px;
    font-weight: bold;
}
.note__text {
    margin-top: 20px;
    font-size: 22px;
    font-weight: bold;
}
.note__input {
    display: flex;
    flex-direction: column;
    font-size: 20px;
}
.note__txt {
    width: 350px;
    height: 150px;
    resize: none;
    padding: 20px;
    margin-top: 10px;
}
.note__btn {
    margin: 25px 10px 0 10px;
    width: 150px;
    height: 50px;
    border-radius: 5px;
    background-color: #007bff;
    color: #fff;
    font-size: 20px;
    font-weight: Bold;
    border: none;
    outline: none;
    transition: 0.3s all;
}
.note__btn:hover {
    background-color: rgba(0, 0, 0, 0);
    border: 1px Solid #007bff;
    color: #007bff;
    /* border-radius: 25px; */
    /* transform: scale(0.95); */
}
.note__wrapper {
    width: 390px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.note__priority {
    margin-top: 20px;
    font-size: 22px;
    font-weight: bold;
}
.note__priority_radio {
    margin-top: 10px;
}
.note__group_radio {
    margin-top: 10px;
}
.note__group {
    margin-top: 20px;
    font-size: 22px;
    font-weight: bold;
}
.note__date {
    margin: 20px 0 10px 0;
    font-size: 22px;
    font-weight: bold;
}

</style>
