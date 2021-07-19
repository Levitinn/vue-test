<template>
    <div class="staff-table__row">
        <div class="staff-user">
            <div class="staff-table__cell">
                {{user.name}}
            </div>
            <div class="staff-table__cell">
                {{user.phone}}
            </div>
        </div>
        <div class="user-subs">
            <Person v-for="(sub, idx) in userSubs" :key="idx" :usersList="usersList" :user="sub" class="staff-user"/>

        </div>
    </div>
</template>

<script>
export default {
    name: 'Person',
    props: {
        user: Object,
        usersList: Array
    },

    data() {
        return {
            userData: this.user,
        }
    },
    computed: {
        userSubs(){
            return this.usersList.filter(user => user.chief === this.userData.id)
        }
    }
}
</script>

<style scoped>
    .staff-table__row {
        border-top: 1px solid #eff1f4;
    }
    .staff-table__row, .staff-user {
        display: grid;
        grid: auto-flow / 50% 50%;
        text-decoration: none;    
    }
    .staff-table__body .staff-table__row {
        display: flex;
        flex-direction: column;
    }
    .staff-user .staff-user .staff-table__cell:first-child {
        margin-left: 24px;
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
    }
    .user-subs .user-subs {
        padding-left: 24px;
    }
</style>