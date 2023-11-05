<script setup>
import { ref, onBeforeMount, onMounted, computed } from 'vue';
import CountryService from '@/service/CountryService';

const countryService = new CountryService();
const loading = ref([false, false, false]);
onMounted(() => {
    countryService.getCountries().then((data) => (countries.value = data));
});

const load = (index) => {
    loading.value[index] = true;
    setTimeout(() => (loading.value[index] = false), 1000);
};
</script>

<script>
import Dialog from 'primevue/dialog';
import { useToast } from 'primevue/usetoast';
import { ref, onBeforeMount, onMounted, computed } from 'vue';

export default {
    data() {
        return {
            nombre: '',
            edad: '',
            sueldo:'',
        };
    },
    methods: {
        obtenerDato() {
            axios.get('https://dummy.restapiexample.com/api/v1/employee/1')
                .then((response) => {
                    this.nombre = response.data.employee_name; // Reemplaza 'nombre' con la clave de tus datos
                    this.edad = response.data.employee_age; // Reemplaza 'edad' con la clave de tus datos
                    this.sueldo = response.data.employee_salary;
                })
                .catch((error) => {
                    console.error('Error al obtener datos de la API:', error);
                });
        },
    },
};

</script>

<template>
    <div class="p-grid">
        <Toast />
        <div class="p-col-12">
            <div class="card">
                <Panel header="Consumir una API" style="height: 100%">
                    <Toolbar class="p-mb-4">
                        <template v-slot:start &&  #body="slotProps">
                            <InputText type="text" size="40" placeholder="ID del empleado" style="margin-right: 10px;">
                            </InputText>
                            <Button type="button" class="p-float-label" label="  Buscar" icon="pi pi-search" iconPos="right"
                                :loading="loading[1]" @click="load(1) && obtenerDato()" style="margin-right: 50px;" />
                            <InputText v-model="nombre" type="text" size="40" placeholder="Nombre del empleado"
                                style="margin-right: 10px;">
                            </InputText>
                            <InputText v-model="edad" type="text" size="40" placeholder="Edad del empleado"
                                style="margin-right: 10px;">
                            </InputText>
                            <InputText v-model="sueldo" type="text" size="40" placeholder="Sueldo del empleado"
                                style="margin-right: 10px;">
                            </InputText>
                        </template>
                        <br>
                    </Toolbar>
                    <hr>
                    <DataTable class="p-datatable-gridlines" :paginator="true" :rows="10"
                        paginatorTemplate="FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink CurrentPageReport RowsPerPageDropdown"
                        :rowsPerPageOptions="[5, 10, 25]"
                        currentPageReportTemplate="Visualiando {last} de {totalRecords} lotes en recolección"
                        responsiveLayout="scroll">

                        <Column flield="id" header="ID Empleado" :sortable="true" style="width:10px"></Column>
                        <Column flield="nomEmp" header="Nombre del empleado" style="width:50px"></Column>
                        <Column flield="edadE" header="Edad del Empleado" style="width:50px"></Column>
                        <Column flield="sueldoE" header="Sueldo del Empleado" style="width:50px" dataType="numeric">
                        </Column>
                    </DataTable>
                </Panel>
            </div>
        </div>
    </div>
</template>
