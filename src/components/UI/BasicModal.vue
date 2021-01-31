<template>
    <transition name="modal">
        <div class="modal">
            <div class="modal__wrapper" @click="$emit('modalClose')">
                <div class="modal__content" @click.stop>
                    <div class="modal__header">
                        <p class="modal__title">{{ title || 'Modal title' }}</p>
                        <button @click="$emit('modalClose')" class="modal__close" type="button">&times;</button>
                    </div>
                    <div class="modal__body">
                        <slot name="body">default body 12</slot>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>

export default {
    name: 'BasicModal',
    props: {
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            //isShow: true
        }
    },
    methods: {
        modalClose(e) {
            if (e.key === 'Escape') this.$emit('modalClose');
        }
    },
    mounted() {
        document.body.addEventListener('keyup', this.modalClose);
        //this.$on('hook:beforeDestroy', () => document.body.removeEventListener('keyup', modalClose));
    },
    beforeDestroy() {
        document.body.removeEventListener('keyup', this.modalClose)
    }
}
</script>

<style lang="scss" scoped>
.modal {
    position: relative;

    &__wrapper {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 998;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: rgba(0, 0, 0, .6);
    }

    &__content {
        position: relative;
        z-index: 999;
        max-width: 480px;
        padding: 26px;
        background-color: #fff;
    }

    &__body {

    }

    &__title {
        margin: 0 0 20px 0;
        font-size: 22px;
        font-weight: 700;
    }

    &__close {
        position: absolute;
        top: 10px;
        right: 10px;
        padding: 0;
        font-size: 28px;
        line-height: 1;
        color: #777;
        outline: 0;
        background-color: transparent;
        border: 0;
        cursor: pointer;
        transition: .3s ease;

        &:hover {
            transform: rotate(90deg);
            color: #000;
        }
    }
}

.modal-enter-active,
.modal-leave-active {
    transition: all .3s;
}

.modal-enter-active .modal__content,
.modal-leave-active .modal__content {
    transition: all .3s;
    transform: scale(1);
}


.modal-enter, .modal-leave-to {
    opacity: 0;
}

.modal-enter .modal__content, .modal-leave-to .modal__content {
    transform: scale(.5);
}
</style>