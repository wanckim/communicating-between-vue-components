<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User name: {{ switchName() }}</p>
        <p>User age: {{ userAge }}</p>
        <button @click="resetName">Reset name</button>
    </div>
</template>

<script>
    import { eventBus } from '../main';

    export default {
        props: {
            myName: {
              type: String
            },
            userAge: Number
        },
        methods: {
            switchName() {
                return this.myName.split('').reverse().join('');
            },
            resetName() {
                this.myName = 'Wan';
                this.$emit('nameWasReset', this.myName);
            }
        },
        created() {
            eventBus.$on('ageWasEditted', (data) => {
                this.userAge = data;
            });
        }
    }
</script>

<style scoped>
    div {
        background-color: lightcoral;
    }
</style>
