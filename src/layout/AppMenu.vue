<script setup>
import { ref } from 'vue';

import AppMenuItem from './AppMenuItem.vue';

const model = ref([
    {
        label: 'Home',
        items: [{ label: 'Dashboard', icon: 'pi pi-fw pi-home', to: '/' }]
    },
    {   //hotel disfruta tu estancia
        label: 'Opciones',
        items: [
            {
                label: 'Clientes',
                icon: 'pi pi-fw pi-user',
                items: [
                    {
                        label: 'Alta Clientes',
                        icon: 'pi pi-fw pi-sign-in',
                        to: '/clientes/altac'
                    },
                    {
                        label: 'Reservacion',
                        icon: 'pi pi-fw pi-times-circle',
                        to: '/clientes/verc'
                    },
                    {
                        label: 'Facturacion',
                        icon: 'pi pi-fw pi-times-circle',
                        to: '/clientes/eliminarc'
                    }//,
                    //{
                    //    label: 'Modificar Cliente',
                    //    icon: 'pi pi-fw pi-lock',
                    //    to: '/auth/modificarc'
                    //}
                ]
            }
        ]
    },
    {
        label: 'Futuro uso',
        icon: 'pi pi-fw pi-briefcase',
        to: '/pages',
        items: [
            {
                label: 'Landing',
                icon: 'pi pi-fw pi-globe',
                to: '/landing'
            },
            {
                label: 'Auth',
                icon: 'pi pi-fw pi-user',
                items: [
                    {
                        label: 'Login',
                        icon: 'pi pi-fw pi-sign-in',
                        to: '/auth/login'
                    },
                    {
                        label: 'Error',
                        icon: 'pi pi-fw pi-times-circle',
                        to: '/auth/error'
                    },
                    {
                        label: 'Access Denied',
                        icon: 'pi pi-fw pi-lock',
                        to: '/auth/access'
                    }
                ]
            },
            {
                label: 'Crud',
                icon: 'pi pi-fw pi-pencil',
                to: '/pages/crud'
            },
            {
                label: 'Not Found',
                icon: 'pi pi-fw pi-exclamation-circle',
                to: '/pages/notfound'
            },
            {
                label: 'Empty',
                icon: 'pi pi-fw pi-circle-off',
                to: '/pages/empty'
            }
        ]
    }
]);
</script>

<template>
    <ul class="layout-menu">
        <template v-for="(item, i) in model" :key="item">
            <app-menu-item v-if="!item.separator" :item="item" :index="i"></app-menu-item>
            <li v-if="item.separator" class="menu-separator"></li>
        </template>
    </ul>
</template>

<style lang="scss" scoped></style>
