<template>
    <div>
        <select @change="updateSalutation">
            <option value>-</option>
            <option v-for="item in salutations" :key="item" :value="item">{{
                item
            }}</option>
        </select>

        <input type="text" @input="updateName" />
    </div>
</template>

<script>
const salutations = ['Ms.', 'Mrs.', 'Miss', 'Mr.', 'Dr.']

export default {
    name: 'SalutationName',

    props: {
        salutation: {
            type: String,
            default: '',
        },

        salutationModifiers: {
            type: Object,
            default: () => ({}),
        },

        name: {
            type: String,
            default: '',
        },

        nameModifiers: {
            type: Object,
            default: () => ({}),
        },
    },

    setup(props, { emit }) {
        const updateSalutation = event => {
            let val = event.target.value

            if (props.salutationModifiers.capitalize) {
                val = val.toUpperCase()
            }

            emit('update:salutation', val)
        }

        const updateName = event => {
            let val = event.target.value

            if (props.nameModifiers.capitalize) {
                val = val.charAt(0).toUpperCase() + val.slice(1)
            }

            if (props.nameModifiers.reverse) {
                val = val
                    .split('')
                    .reverse()
                    .join('')
            }

            emit('update:name', val)
        }

        return {
            salutations,
            updateSalutation,
            updateName,
        }
    },
}
</script>

<style lang="scss" scoped>
div {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}
select {
    margin-right: 0.5rem;
}
input {
    width: 50%;
}
</style>
