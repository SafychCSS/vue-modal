<template>
    <BasicModal title="Modal with form + validate" @modalClose="$emit('close')">
        <div class="form" slot="body">
            <form @submit.prevent="onSubmit">
                <div
                    class="form__block"
                    :class="{ 'form__block--error': $v.name.$error }"
                >
                    <label class="form__label" for="name">Your name</label>

                    <div class="error" v-if="!$v.name.required">Field is required</div>
                    <div class="error" v-if="!$v.name.minLength">Name must have at least {{$v.name.$params.minLength.min}} letters.</div>

                    <input
                        :class="{ 'form__input--error': $v.name.$error }"
                        v-model="$v.name.$model"
                        class="form__input"
                        id="name"
                        type="text"
                        placeholder="Enter your name">
                </div>
                <div class="form__block"
                     :class="{ 'form__block--error': $v.email.$error }">
                    <label class="form__label" for="email">Your email</label>

                    <div class="error" v-if="!$v.email.required">Field is required</div>
                    <div class="error" v-if="!$v.email.email">Email is incorrect</div>

                    <input
                        :class="{ 'form__input--error': $v.email.$error }"
                        v-model="$v.email.$model"
                        class="form__input"
                        id="email"
                        type="text"
                        placeholder="Enter your email">
                </div>
                <button class="btn btn--basic btn--success">Send form</button>
            </form>
        </div>
    </BasicModal>
</template>

<script>
import { required, minLength, email } from 'vuelidate/lib/validators';

import BasicModal from "@/components/UI/BasicModal";

export default {
    name: 'ModalValidate',
    components: {
        BasicModal
    },
    data() {
        return {
            name: '',
            email: ''
        }
    },
    validations: {
        name: {
            required,
            minLength: minLength(7),
        },
        email: {
            email,
            required,
        }
    },
    methods: {
        onSubmit() {
            this.$v.$touch();
            if (!this.$v.$invalid) {
                const user = {
                    name: this.name,
                    email: this.email
                }

                // Done
                console.log(user);
                this.name = this.email = '';
                this.$v.$reset();
                this.$emit('close');
            }
        }
    }
}
</script>

<style scoped>

</style>