<template>
    <ion-page>
        <ion-header>
            <ion-toolbar>
                <ion-title>Registro</ion-title>
                <ion-buttons slot="end">
                    <ion-button  fill="solid" @click="router.push({ name: 'Login' })">Login</ion-button>
                </ion-buttons>
            </ion-toolbar>
        </ion-header>
        <ion-content class="ion-padding">
            <h2>Crear Cuenta</h2>
            
            <ion-input 
                class="ion-margin-top"
                label="Usuario" 
                label-placement="floating" 
                fill="outline" 
                placeholder="Escribe aquí tu usuario"
                v-model="userStore.registro.usuario">
            </ion-input>

            <ion-input 
                class="ion-margin-top"
                label="Email" 
                label-placement="floating" 
                fill="outline" 
                type="email"
                placeholder="Escribe aquí tu email"
                v-model="userStore.registro.email">
            </ion-input>

            <ion-input 
                class="ion-margin-top"
                label="Contraseña" 
                label-placement="floating" 
                fill="outline" 
                placeholder="Escribe aquí tu contraseña"
                v-model="userStore.registro.password"
                type="password">
            </ion-input>

            <ion-button expand="block" class="ion-margin-top" @click="registrarse()">Registrarse</ion-button>
        </ion-content>
    </ion-page>
</template>
<script setup lang="ts">
import { IonContent, IonHeader, IonTitle, IonToolbar, IonPage, IonInput, 
    IonButtons, IonButton, alertController } from '@ionic/vue';
import { useRouter } from 'vue-router';
import { useUserStore } from '@/stores/user';

const router = useRouter();
const userStore = useUserStore();

function registrarse() {
    userStore.$registro().then(response => {
        console.log(response);
        router.push({ name: 'Seccion' });
    }).catch(error => {
        alertController.create({
            header: 'Error',
            message: error.response.data.message,
            buttons: ['Continuar']
        }).then(alert => alert.present());
    });     
}
</script>

<style scoped>
ion-input {
    display: block;
    margin-bottom: 16px;
}
</style>