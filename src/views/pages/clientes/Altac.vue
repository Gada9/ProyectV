<script setup>
import { ref } from 'vue';

const dropdownItems = ref([
    { name: 'Opción 1', code: 'Opción 1' },
    { name: 'Opción 2', code: 'Opción 2' },
    { name: 'Opción 3', code: 'Opción 3' }
]);

const dropdownItem = ref(null);

const cliente = ref({
    nombre: '',
    ap_pat: '',
    ap_mat: '',
    telefono: '',
    rfc: '',
    email: '',
    direccion: ''
});

const clientes = ref([]);
const editIndex = ref(null);

const guardarCliente = () => {
    if (cliente.value.nombre && cliente.value.ap_pat) {
        if (editIndex.value !== null) {
            // Actualizar cliente existente
            clientes.value[editIndex.value] = { ...cliente.value };
            editIndex.value = null; // Salir del modo de edición
        } else {
            // Añadir nuevo cliente
            clientes.value.push({ ...cliente.value });
        }
        limpiarFormulario();
    } else {
        alert("Por favor, completa los campos requeridos.");
    }
};

const editarCliente = (index) => {
    const clienteEditado = clientes.value[index];
    cliente.value = { ...clienteEditado };
    editIndex.value = index;
};

const eliminarCliente = (index) => {
    clientes.value.splice(index, 1);
};

const limpiarFormulario = () => {
    cliente.value = {
        nombre: '',
        ap_pat: '',
        ap_mat: '',
        telefono: '',
        rfc: '',
        email: '',
        direccion: ''
    };
    editIndex.value = null;
};
</script>

<template>
    <Fluid>
        <div class="card flex flex-col gap-4 w-full">
            <div class="font-semibold text-xl">Alta de Cliente</div>
            <div class="flex flex-wrap gap-4">
                <div class="w-full md:w-1/3">
                    <label for="nombre">Nombre</label>
                    <InputText id="nombre" type="text" v-model="cliente.nombre" class="w-full"/>
                </div>
                <div class="w-full md:w-1/3">
                    <label for="ap_pat">Apellido Paterno</label>
                    <InputText id="ap_pat" type="text" v-model="cliente.ap_pat" class="w-full"/>
                </div>
                <div class="w-full md:w-1/3">
                    <label for="ap_mat">Apellido Materno</label>
                    <InputText id="ap_mat" type="text" v-model="cliente.ap_mat" class="w-full"/>
                </div>
                <div class="w-full md:w-1/3">
                    <label for="telefono">Teléfono</label>
                    <InputText id="telefono" type="text" v-model="cliente.telefono" class="w-full"/>
                </div>
                <div class="w-full md:w-1/3">
                    <label for="rfc">RFC</label>
                    <InputText id="rfc" type="text" v-model="cliente.rfc" class="w-full"/>
                </div>
                <div class="w-full md:w-1/3">
                    <label for="email">Email</label>
                    <InputText id="email" type="text" v-model="cliente.email" class="w-full"/>
                </div>
                <div class="w-full">
                    <label for="direccion">Dirección</label>
                    <Textarea id="direccion" rows="2" v-model="cliente.direccion" class="w-full"/>
                </div>
            </div>
            <Button label="Guardar Cliente" @click="guardarCliente" class="mt-4">
                {{ editIndex !== null ? "Actualizar" : "Guardar" }}
            </Button>
        </div>

        <div class="mt-8 card flex flex-col gap-4 w-full">
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
                        <th class="px-4 py-2">Acciones</th>
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
                        <td class="border px-4 py-2">
                            <Button icon="pi pi-pencil" @click="editarCliente(index)" class="mr-2"></Button>
                            <Button icon="pi pi-trash" @click="eliminarCliente(index)" class="p-button-danger"></Button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </Fluid>
</template>
