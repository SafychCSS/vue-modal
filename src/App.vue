<template>
    <div id="app">
        <div class="container">
            <button @click="firstModal = !firstModal" class="btn btn--basic btn--primary" type="button">open modal</button>
            <BasicModal @modalClose="modalClose" v-if="firstModal" title="Title modal">
                <template v-slot:body>
                    <p>modal body</p>
                    <button class="btn btn--basic">btn</button>
                </template>
            </BasicModal>
        </div>
    </div>
</template>

<script>

import BasicModal from "@/components/BasicModal";

export default {
    name: 'App',
    components: {
        BasicModal
    },
    data() {
        return {
            firstModal: false
        }
    },
    methods: {
        modalClose() {
            this.firstModal = false;
        }
    }
}
</script>

<style>

</style>
