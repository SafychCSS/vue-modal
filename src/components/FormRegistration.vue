<template>
    <BasicModal :title="title" @modalClose="$emit('close')">
        <div class="form" slot="body">
            <form @submit.prevent="onSubmit">
                <div class="form__block"
                     :class="{ 'form__block--error': $v.user.email.$error }"
                >
                    <label class="form__label" for="email">Your email</label>
                    <div class="error"
                         v-if="!$v.user.email.required">
                        Field is required
                    </div>
                    <div class="error" v-if="!$v.user.email.email">Email is incorrect</div>
                    <input
                        v-model="$v.user.email.$model"
                        class="form__input"
                        id="email"
                        type="email"
                        placeholder="Enter your email">
                </div>

                <div class="form__block" :class="{ 'form__block--error': $v.user.password.$error }">
                    <label class="form__label" for="password">Your password</label>
                    <div class="error"
                         v-if="!$v.user.password.required">
                        Field is required
                    </div>
                    <div class="error" v-if="!$v.user.password.minLength">
                        Password must have at least {{ $v.user.password.$params.minLength.min }} letters.
                    </div>
                    <input
                        v-model="$v.user.password.$model"
                        class="form__input"
                        id="password"
                        type="password"
                        placeholder="Enter your password">
                </div>

                <div
                    class="form__block"
                    :class="{ 'form__block--error': $v.user.repeatPassword.$error }"
                >
                    <label class="form__label" for="repeatPassword">Repeat password</label>
                    <div class="error" v-if="!$v.user.repeatPassword.sameAsPassword">
                        Passwords must be identical.
                    </div>
                    <input
                        v-model.trim="$v.user.repeatPassword.$model"
                        class="form__input"
                        id="repeatPassword"
                        type="password"
                        placeholder="Repeat your password">
                </div>

                <button @click="" class="btn btn--basic btn--success">Send form</button>
            </form>
            <a href="#" @click.prevent="openLogin">sign in</a>
        </div>
    </BasicModal>
</template>

<script>
import { required, email, minLength, sameAs } from 'vuelidate/lib/validators';
import BasicModal from "@/components/UI/BasicModal";

export default {
    name: 'FormRegistration',
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
                password: '',
                repeatPassword: ''
            }
        }
    },
    validations: {
        user: {
            email: {
                required,
                email
            },
            password: {
                required,
                minLength: minLength(6)
            },
            repeatPassword: {
                sameAsPassword: sameAs('password')
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
                    repeatPassword: this.user.repeatPassword,
                });
                this.user.email = '';
                this.user.password = '';
                this.user.repeatPassword = '';

                this.$v.$reset();
                this.$emit('close');
            }
        },
        openLogin() {
            this.$emit('close');
            this.$emit('openLogin');
        }
    }
}
</script>

<style scoped>

</style>