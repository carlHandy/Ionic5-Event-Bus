<template>
    <ion-page>
        <ion-header class="ion-no-border">
            <ion-toolbar color="primary">
                <ion-title>Booking Details</ion-title>
            </ion-toolbar>
                <ion-text>
                    <p style="text-align: center; text-transform: none !important; color: white;">
                        Fill in the form below to book your home improvement.
                    </p>
                </ion-text>
        </ion-header>
        <ion-content>
            <ion-card scroll-y="true">
                <div style="margin-top: 25px;"/>
                <ion-text>
                </ion-text>             
                <ion-radio-group value="Business">
                    <ion-item>
                        <ion-label>Business</ion-label>
                        <ion-radio id="business" slot="start" value="Business"/>
                    </ion-item>
                    <ion-item>
                        <ion-label>Residential</ion-label>
                        <ion-radio id="residential" slot="start" value="Residential"/>
                    </ion-item>
                </ion-radio-group>
                <ion-item>
                    <ion-label position="stacked">Company Name</ion-label>
                    <ion-input autofocus="true" type="text" pattern="text" placeholder="Company Name"/>
                </ion-item>
                <ion-item>
                    <ion-label position="stacked">Contact Name</ion-label>
                    <ion-input autofocus="true" type="text" required="true" pattern="text" placeholder="John Doe"/>
                </ion-item>
                <ion-item>
                    <ion-label position="stacked">Email</ion-label>
                    <ion-input autofocus="true" type="email"  required="true"
                        inputmode="email" pattern="email" clearInput="true" placeholder="your@email.com"/>
                </ion-item>
                <ion-item>
                    <ion-label position="stacked">Telephone</ion-label>
                    <ion-input autofocus="true" type="number" required="true" max="7"
                        inputmode="tel" maxlength="7" pattern="number" placeholder="6150193"/>
                </ion-item>
                <ion-item>
                    <ion-label position="stacked">Address</ion-label>
                    <ion-textarea placeholder="Enter address here" />
                </ion-item>
                <ion-grid>
                    <ion-row>
                        <ion-col>
                            <ion-button expand="block" shape="round"> Confirm Booking
                            </ion-button>
                        </ion-col>
                    </ion-row>
                    <ion-row>
                        <ion-col>
                            <ion-button expand="block" shape="round" color="danger"
                                routerDirection="forward" routerLink="/tabs/tab1"
                            > Cancel
                            </ion-button>
                        </ion-col>
                    </ion-row>
                </ion-grid>
            </ion-card>
        </ion-content>
    </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonButton, IonContent,
    IonCard, IonText, IonTitle, IonItem, IonInput, IonLabel, IonGrid, IonRow, IonCol,
    IonRadio, IonRadioGroup, IonTextarea,
  onIonViewDidEnter,
    } from '@ionic/vue';
import eventBus from './eventBus';

export default {
    components: {
        IonPage, IonHeader, IonToolbar, IonButton, IonContent,
        IonCard, IonText, IonTitle, IonItem, IonInput, IonLabel, IonGrid, IonRow, IonCol,
        IonRadio, IonRadioGroup, IonTextarea
    },
    setup() {
 
        onIonViewDidEnter(() => {
            eventBus().emitter.on('service-event', (payload) => {
                console.log('service-event', payload);

            })
        });

        return {  }
        
    },
}
</script>

<style scoped>
ion-header {
    background: #3880ff;
}
ion-card {
    border-top-right-radius: 25px;
    border-top-left-radius: 25px;
    border-bottom-right-radius: 0px;
    border-bottom-left-radius: 0px;
    height: 100%;
    width: 100%;
    margin: 0%;
    overflow: scroll;
    position: absolute;
}

ion-content {
    --background:#3880ff;
}
</style>