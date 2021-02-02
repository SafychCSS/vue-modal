<template>
    <BasicModal :title="title" @modalClose="$emit('close')">
        <div class="form" slot="body">
            <form @submit.prevent="onSubmit">
                <div class="form__block" :class="{ 'form__block--error': $v.user.email.$error }">
                    <label class="form__label" for="email">Your email</label>
                    <div class="error" v-if="!$v.user.email.required">Field is required</div>
                    <div class="error" v-if="!$v.user.email.email">Email is incorrect</div>
                    <input v-model="$v.user.email.$model" class="form__input" id="email" type="text" placeholder="Enter your email">
                </div>
                <div class="form__block">
                    <label class="form__label" for="password">Your password</label>
                    <input v-model="user.password" class="form__input" id="password" type="email" placeholder="Enter your password">
                </div>
                <button class="btn btn--basic btn--success">Send form</button>
            </form>
            <a href="#" @click.prevent="openRegistration">sign up</a>
        </div>
    </BasicModal>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators';
import BasicModal from "@/components/UI/BasicModal";

export default {
    name: 'FormLogin',
    components: {
        BasicModal
    },
    props: {
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            user: {
                email: '',
                password: ''
            }
        }
    },
    validations: {
        user: {
            email: {
                required,
                email
            }
        }
    },
    methods: {
        onSubmit() {
            this.$v.$touch();
            if (!this.$v.$invalid) {
                console.log({
                    email: this.user.email,
                    password: this.user.password,
                });
                this.user.email = '';
                this.user.password = '';

                this.$v.$reset();
                this.$emit('close');
            }
        },
        openRegistration() {
            this.$emit('close');
            this.$emit('openReg');
        }
    }
}
</script>