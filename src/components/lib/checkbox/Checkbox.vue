<template>
    <div class="checkbox-wrapper">
        <div v-for="(checkbox, i) in checkboxes" 
            :key="i"
            class="checkbox-block">
            <input type="checkbox" 
                   :value="checkbox" 
                   v-model="selected" />
            <label :for="checkbox">
                {{checkbox}}
            </label>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Checkbox',
    props: {
        checkboxes: {
            type: Array
        },
        value: {
            type: Array
        }
    },
    data () {
        return {
            selected: []
        }
    },
    watch: {
        selected() {
            this.$emit('selected', this.selected);
        }
    }
}
</script>
<style scoped>
    .checkbox-wrapper {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }
</style>