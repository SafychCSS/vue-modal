<template>
    <div id="app">
        <div class="container">
            <button
                @click="modalSimple = !modalSimple"
                class="btn btn--basic btn--primary"
                type="button"
            >
                open simple modal
            </button>

            <button
                @click="modalForm.isShow = !modalForm.isShow"
                class="btn btn--basic btn--primary"
                type="button"
            >
                open modal with form
            </button>

            <button
                @click="modalValidate.isShow = !modalValidate.isShow"
                class="btn btn--basic btn--primary"
                type="button"
            >
                open modal with form + validate
            </button>
            <button
                @click="modalLogin.isShow = !modalLogin.isShow"
                class="btn btn--basic btn--primary"
                type="button"
            >
                Login form
            </button>
            <BasicModal @modalClose="modalClose('modalSimple')" v-show="modalSimple" title="Title modal">
                <template v-slot:body>
                    <p>simple modal</p>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Maiores, quo.</p>
                </template>
            </BasicModal>

            <BasicModal @modalClose="modalClose('modalForm', 'isShow')" v-show="modalForm.isShow" title="Modal with form">
                <div class="form" slot="body">
                    <form @submit.prevent>
                        <div class="form__block">
                            <label class="form__label" for="name">Your name</label>
                            <input v-model="modalForm.name" class="form__input" id="name" type="text" placeholder="Enter your name">
                        </div>
                        <div class="form__block">
                            <label class="form__label" for="email">Your email</label>
                            <input v-model="modalForm.email" class="form__input" id="email" type="email" placeholder="Enter your email">
                        </div>
                        <button class="btn btn--basic btn--success">Send form</button>
                    </form>
                </div>
            </BasicModal>

            <ModalValidate v-show="modalValidate.isShow" @close="modalClose('modalValidate', 'isShow')"></ModalValidate>

            <FormLogin title="Sign in" v-show="modalLogin.isShow" @close="modalClose('modalLogin', 'isShow')" @openReg="modalRegistration.isShow = true"/>

            <FormRegistration title="Sign up" v-show="modalRegistration.isShow" @close="modalClose('modalRegistration', 'isShow')" @openLogin="modalLogin.isShow = true"/>

        </div>
    </div>
</template>

<script>

import BasicModal from "@/components/UI/BasicModal";
import ModalValidate from "@/components/ModalValidate";
import FormLogin from "@/components/FormLogin";
import FormRegistration from "@/components/FormRegistration";

export default {
    name: 'App',
    components: {
        BasicModal,
        ModalValidate,
        FormLogin,
        FormRegistration
    },
    data() {
        return {
            modalSimple: false,
            modalForm: {
                isShow: false,
                name: '',
                email: ''
            },
            modalValidate: {
                isShow: false
            },
            modalLogin: {
                isShow: false
            },
            modalRegistration: {
                isShow: false
            }
        }
    },
    methods: {
        modalClose(...args) {
            if (args.length === 1)
                this[args[0]] = false;
            else
                this[args[0]][args[1]] = false;
        },
    }
}
</script>
