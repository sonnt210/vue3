<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>At least on input value is invalid</p>
            <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">
                Okay
            </base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" cols="30" rows="4" ref="descInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="linkInput">
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data() {
        return {
            inputIsInvalid: false,
        }
    },
    methods: {
        submitData() {
            const enterdTitle = this.$refs.titleInput.value;
            const enterdDesc = this.$refs.descInput.value;
            const enterdUrl = this.$refs.linkInput.value;

            if(enterdTitle.trim() === '' || enterdDesc.trim() === '' || enterdUrl.trim() === '') {
                this.inputIsInvalid = true;
                return;
            }

            this.addResource(enterdTitle, enterdDesc, enterdUrl);
        },
        confirmError() {
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>