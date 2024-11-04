<script setup>
import { ref } from 'vue';

const dropdownItems = ref([
    { name: 'Opción 1', code: 'Opción 1' },
    { name: 'Opción 2', code: 'Opción 2' },
    { name: 'Opción 3', code: 'Opción 3' }
]);

const dropdownItem = ref(null);

// Referencias para los campos del cliente
const cliente = ref({
    nombre: '',
    ap_pat: '',
    ap_mat: '',
    telefono: '',
    rfc: '',
    email: '',
    direccion: ''
});

// Arreglo para almacenar los clientes
const clientes = ref([]);

// Función para manejar el envío del formulario
const guardarCliente = () => {
    if (cliente.value.nombre && cliente.value.ap_pat) {
        // Agregar el cliente al arreglo
        clientes.value.push({ ...cliente.value });
        
        // Limpiar los campos
        cliente.value = {
            nombre: '',
            ap_pat: '',
            ap_mat: '',
            telefono: '',
            rfc: '',
            email: '',
            direccion: ''
        };
    } else {
        alert("Por favor, completa los campos requeridos.");
    }
};
</script>

<template>
    <Fluid>
        <div class="flex flex-col md:flex-row gap-8">
            <div class="md:w-1/2 w-full">
                <div class="card flex flex-col gap-4">
                    <div class="font-semibold text-xl">Alta de Cliente</div>
                    <div class="flex flex-col gap-2">
                        <label for="nombre">Nombre</label>
                        <InputText id="nombre" type="text" v-model="cliente.nombre" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="ap_pat">Apellido Paterno</label>
                        <InputText id="ap_pat" type="text" v-model="cliente.ap_pat" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="ap_mat">Apellido Materno</label>
                        <InputText id="ap_mat" type="text" v-model="cliente.ap_mat" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="telefono">Teléfono</label>
                        <InputText id="telefono" type="text" v-model="cliente.telefono" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="rfc">RFC</label>
                        <InputText id="rfc" type="text" v-model="cliente.rfc" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="email">Email</label>
                        <InputText id="email" type="text" v-model="cliente.email" />
                    </div>
                    <div class="flex flex-col gap-2">
                        <label for="direccion">Dirección</label>
                        <InputText id="direccion" type="text" v-model="cliente.direccion" />
                    </div>
                    <Button label="Guardar Cliente" @click="guardarCliente" class="mt-4"></Button>
                </div>
            </div>
        </div>

        <div class="mt-8">
            <div class="card flex flex-col gap-4 w-full">
                <div class="font-semibold text-xl">Lista de Clientes</div>
                <table class="table-auto w-full">
                    <thead>
                        <tr>
                            <th class="px-4 py-2">Nombre</th>
                            <th class="px-4 py-2">Apellido Paterno</th>
                            <th class="px-4 py-2">Apellido Materno</th>
                            <th class="px-4 py-2">Teléfono</th>
                            <th class="px-4 py-2">RFC</th>
                            <th class="px-4 py-2">Email</th>
                            <th class="px-4 py-2">Dirección</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(cliente, index) in clientes" :key="index">
                            <td class="border px-4 py-2">{{ cliente.nombre }}</td>
                            <td class="border px-4 py-2">{{ cliente.ap_pat }}</td>
                            <td class="border px-4 py-2">{{ cliente.ap_mat }}</td>
                            <td class="border px-4 py-2">{{ cliente.telefono }}</td>
                            <td class="border px-4 py-2">{{ cliente.rfc }}</td>
                            <td class="border px-4 py-2">{{ cliente.email }}</td>
                            <td class="border px-4 py-2">{{ cliente.direccion }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </Fluid>
</template>
