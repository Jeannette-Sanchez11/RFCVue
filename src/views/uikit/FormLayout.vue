<script setup>
import { ref } from 'vue';
import InputMask from 'primevue/inputmask'; //para el formato de fecha

const dropdownItems = ref([
    { name: 'Option 1', code: 'Option 1' },
    { name: 'Option 2', code: 'Option 2' },
    { name: 'Option 3', code: 'Option 3' }
]);

const dropdownItem = ref(null);
</script>

<template>
    <div class="grid">
        <div class="col-12 md:col-11">
            <div class="card p-fluid">
                <h3>GENERAR RFC DE UNA PERSONA</h3>
                <div class="field">
                    <label for="name1">Nombre(s):</label>
                    <InputText id="name1" type="text" />
                </div>
                <div class="field">
                    <label for="email1">Apellido Paterno:</label>
                    <InputText id="email1" type="text" />
                </div>
                <div class="field">
                    <label for="apPat">Apellido Materno:</label>
                    <InputText id="apPat" type="text" />
                </div>
                <div class="field">
                    <label for="apPat">Fecha de nacimiento:</label>
                    <InputMask id="basic" v-model="value" mask="99/99/9999" placeholder="dd/mm/aaaa" />
                </div>
                <div class="field">
                    <label for="age1">RFC</label>
                    <InputText id="age1" type="text" />
                </div>
                <div class="col-12 md:col-5">
                    <Button label="Generar" class="p-button-raised p-button-success mr-2 mb-2"></Button>
                </div>
            </div>

        </div>

    </div>
</template>
