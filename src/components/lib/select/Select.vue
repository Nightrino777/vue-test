<template>
    <div>
        <select v-model="selectColor">
            <option v-for="option in options" 
                    :key="option"
                    :value="option">
                    {{option}} </option>
        </select>
    </div>
</template>
<script>
export default {
    name: 'Select',
    props: {
        options: {
            type: Array
        }
    },
    data () {
        return {
            selectColor: 'All'
        }
    },
    watch: {
        selectColor() {
            this.$emit('selectedColor', this.selectColor);
        }
    }
}
</script>