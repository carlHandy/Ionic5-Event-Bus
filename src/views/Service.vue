<template v-slot:start>
    <ion-page>
        <ion-header class="ion-no-border">
            <ion-toolbar>
                <ion-buttons>
                    <ion-back-button defaultHref="/tabs/home"></ion-back-button>
                </ion-buttons>
                <ion-title style="text-transform: uppercase;">Service Details</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content>
            <div>
                <ion-img src="https://via.placeholder.com/414" />
            </div>            
            <ion-grid>
                <ion-row style="text-align: center;">
                    <ion-col>
                        <h2>Category Name</h2>
                        <ion-text>
                            <p style="color: grey;">Lorem Ipsum is not simply dummy text</p>
                        </ion-text>
                    </ion-col>
                </ion-row>
                <ion-row >
                    <ion-col>
                        <h4 style="text-align: center;">Select service(s) to continue</h4>
                        <p>
                            <ion-chip v-for="service of services" :key="service.id"
                            :color="color[service.id]" @click="updateServiceState(service.id); onSelect(service)"                              
                            >
                                <ion-label>{{service.name}}</ion-label>
                                <ion-icon :icon="icon[service.id]"></ion-icon>
                            </ion-chip>
                        </p>
                    </ion-col>
                </ion-row>
                <ion-row style="text-align: center;">
                    <ion-col>
                        <ion-button routerDirection="forward" routerLink="/tabs/tab2" 
                            expand="block" shape="round"  @click="sendEvent">Book Now
                        </ion-button>
                    </ion-col>
                </ion-row>
            </ion-grid>
        </ion-content>
    </ion-page>
</template>

<script>
/* eslint-disable*/
import { IonPage, IonHeader, IonToolbar, IonButtons, IonButton, IonBackButton, IonTitle, IonContent, IonImg,
    IonGrid, IonRow, IonCol, IonChip, IonLabel, IonText, IonIcon } from '@ionic/vue';
import { addOutline, checkmark } from 'ionicons/icons';
import { reactive, toRefs } from 'vue';
import eventBus from './eventBus';

export default {
    components: {
        IonPage,
        IonHeader,
        IonToolbar,
        IonButtons,
        IonButton,
        IonBackButton,
        IonTitle,
        IonContent,
        IonImg,
        IonGrid,
        IonRow,
        IonCol, 
        IonChip,
        IonLabel,
        IonText,
        IonIcon
    },
    props: ['name'],
    setup() {

        const chipState = reactive({
            // temporary hack - should be dynamic instead of hardcoded to the number of services
            icon: [addOutline, addOutline, addOutline, addOutline ],
            color: ['tertiary', 'tertiary', 'tertiary', 'tertiary'],
        })
        
        const clickedItems = [];

        const services = [
            {
                id: 1,
                name: 'Painting'
            },
            {
                id: 2,
                name: 'Bathroom Remodeling'
            },
            {
                id: 3,
                name: 'Tiling'
            }
        ]

        function onSelect(service) {    
            if (chipState.color[service.id] === 'success') {
                clickedItems.push(service);
            } else {
                const clickedItemsIndex = clickedItems.indexOf(service);
                if(clickedItemsIndex !== -1) {
                    clickedItems.splice(clickedItemsIndex, 1);
                }
            }
        }

        const updateServiceState =  (i) => {
            if(chipState.icon[i] == addOutline) {
                chipState.icon[i] = checkmark;
                chipState.color[i] = 'success';
            } else {
                chipState.icon[i] = addOutline;
                chipState.color[i] = 'tertiary';
            }
        }
        // emit event
        const sendEvent = async () => {
            eventBus().emitter.emit('service-event', clickedItems );
            console.log('emiiter', clickedItems);
        }

        return { ...toRefs(chipState), onSelect, updateServiceState, sendEvent, services }
    },
}
</script>

<style scoped>
ion-button {
    --background: #ff834f;
}
</style>