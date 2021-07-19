<template>
    <div class="staff__modal">
        <button 
            @click="openModal = !openModal" 
            class="add-person base-btn"
            >Добавить
        </button>
        <div v-if="openModal" class="add-person__overlay">
            <div class="add-person__modal">
                <h2 class="modal__title">{{ title }}</h2>
                <div 
                    @click="openModal = !openModal"
                    class="modal__close">
                </div>
                <form class="modal__form">
                    <label class="form__label">
                        <span class="label__title">Имя</span>
                        <input type="text" v-model="userName" class="form-input base-input">
                    </label>
                    <label class="form__label">
                        <span class="label__title">Телефон</span>
                        <input type="tel" v-model="userPhone" class="form-input base-input">
                    </label>
                    <label class="form__label" v-if="users.length">
                        <span class="label__title">Начальник</span>
                        <select name="chief" v-model="selectChief" id="chief" class="base-input">
                            <option disabled selected>Выберите руководителя</option>
                            <option v-for="(user, idx) in users" :key="idx" :value="user.id">{{ user.name }}</option>
                        </select>
                    </label>
                    <button 
                        @click.prevent="getUserData"
                        class="base-btn modal-btn">
                        Сохранить
                    </button>
                </form>
            </div>
        </div>   
    </div>
</template>

<script>
    import { v4 as uuidv4 } from 'uuid';
    export default {
        name: 'StaffAddPerson',
        props: {
            title: String,
            users: Array
        },
        
        emits: ['addUser'],
        data() {
            return {
                userName: '',
                userPhone: '',
                selectChief: '',
                openModal: false,
            }
        },
        computed: {

        },
        methods: {
            getUserData() {
                const userData = {
                    name: this.userName,
                    phone: this.userPhone,
                    chief: this.selectChief,
                    id: uuidv4()
                }
                this.$emit('add-user', userData);
                this.clearModal();
                this.openModal = false;
            },

            clearModal() {
                this.userName = '';
                this.userPhone = '';
                this.selectChief = '';
            }

        }
    }
</script>

<style scoped>
    .staff__modal {
        text-align: right;
    }
    .add-person__overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: rgb(0 0 0 / 35%);
    }
    .add-person__modal {
        background-color: #fff;
        padding: 16px 24px;
        margin-top: 20vh;
        position: relative;
    }
    .modal__form {
        width: 400px;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }
    .form__label {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 8px;
    }
    .add-person {
        align-self: flex-end;
    }
    .modal-btn {
        margin-top: 12px;
    }
    .modal__close {
        width: 20px;
        height: 20px;
        border-radius: 40px;
        position: relative;
        z-index: 1;
        cursor: pointer;
        position: absolute;
        top: 10px;
        right: 10px;
    }
    .modal__close::before {
        content: '+';
        color: #333;
        position: absolute;
        z-index: 2;
        transform: rotate(45deg);
        font-size: 30px;
        line-height: 1;
        top: -5px;
        left: 0;
        transition: all 0.3s cubic-bezier(0.77, 0, 0.2, 0.85);
    }
    .modal__close::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border-radius: 100%;
        background: #333;
        z-index: 1;
        transition: all 0.3s cubic-bezier(0.77, 0, 0.2, 0.85);
        transform: scale(0.01);
    }

</style>