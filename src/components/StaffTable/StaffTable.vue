<template>
    <div class="table-wrapper">
        <StaffAddPerson 
            @add-user="onAddUser" 
            :users="tableData"
            title="Добавление пользователя"/>
        <div v-if="tableData.length" class="staff-table">
            <div data-elem="header" class="staff-table__header staff-table__row">
                <div data-elem="name" @click="sortData" data-sorting="name" class="staff-table__cell">
                    Имя
                </div>
                <div data-elem="phone" @click="sortData" data-sorting="phone" class="staff-table__cell">
                    Телефон
                </div>
            </div>
            <div data-elem="body" class="staff-table__body">
                <Person v-for="(person, idx) in usersTree" :key="idx" :usersList="tableData" :user="person" />
            </div>
        </div>
        <div v-else class="table-placeholder">
            Таблица пуста. Вы можете добавить пользователя
        </div>
    </div>
</template>

<script>

import StaffAddPerson from './StaffAddPerson.vue';
import Person from './Person.vue'
export default {
    name: 'StaffTable',
    components: {
        StaffAddPerson,
        Person
    },

    data() {
        return {
            tableData: [],
        }
    },
    
    created() {
        if( localStorage.getItem('tableData') ) {
            this.tableData = JSON.parse(localStorage.getItem('tableData'))
        }
    },
    
    methods: {
        onAddUser(userData) {
            this.tableData = [...this.tableData,userData]
            this.saveData();
        },

        sortData(event) {
            const field = event.target.getAttribute('data-sorting');
            let sortType = event.target.getAttribute('data-type');
            if (!sortType) {
                sortType = 'asc'
            } 
            const directions = {
                asc: 1,
                desc: -1
            };
            const direction = directions[sortType];
            this.tableData = this.tableData.sort((a, b) => {
                switch (field) {
                case 'phone':
                    return direction * (a[field] - b[field]);
                case 'name':
                    return direction * a[field].localeCompare(b[field], ['ru', 'en']);
                default:
                    return direction * (a[field] - b[field]);
                }
            });
            event.target.setAttribute('data-type', sortType === 'asc' ? 'desc' : 'asc');
        },

        saveData() {
            const jsonUsers = JSON.stringify(this.tableData)
            localStorage.setItem('tableData', jsonUsers)
        }
    },

    computed: {
        usersTree(){
            return this.tableData.filter(user => user.chief === '')
        },
        

    }

}

</script>

<style scoped>
    .staff-table {
        background-color: white;
        max-width: 100%;
        width: 100%;
        border-radius: 4px;
        margin-top: 12px;
        overflow: hidden;
    }
    .staff-table__row, .staff-user, .subs__row {
        display: grid;
        grid: auto-flow / 50% 50%;
        text-decoration: none;    
    }
    .staff-table__body .staff-table__row, .staff__subs {
        display: flex;
        flex-direction: column;
    }
    .staff-table__cell:first-child {
        padding-left: 32px;
    }
    .staff__subs .staff-table__cell:first-child {
        padding-left: 64px;
    }
    .staff-table__cell {
        padding: 16px;
        font-size: 16px;
        line-height: 20px;
        display: flex;
        align-items: center;
        text-align: left;
        text-align: initial;
        border-top: 1px solid #eff1f4;
    }
    .staff-table__header .staff-table__cell {
        color: #c2cfe0;
        border-top: none;
        cursor: pointer;
    }
    .table-placeholder {
        padding: 16px;
        background-color: white;
        border-radius: 4px;
        width: 100%;
        margin-top: 12px;
    }

</style>
