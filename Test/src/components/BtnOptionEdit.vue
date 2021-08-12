<template>
    <td><button @click="actionOption">EDIT</button></td>
</template>

<script>
export default {
    name: 'BtnOptionEdit',
    components: {
    },
    props: {
        option: {
            type: Object
        }
    },
    data: () => {
        return {
        }
    },
    methods: {
        actionOption: function () {
            this.$emit('doAction', { type: 'EDIT', option: this.option });
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>