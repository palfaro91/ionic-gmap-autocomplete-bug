<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>

      <div
        class="w-full flex"
        style="padding-left: 12px; padding-right: 12px; justify-content: center; flex-direction: column; align-items: center; height: 100%;"
      >
        <div>
          <h2>Steps to reproduce:</h2>
          <ol>
            <li>
              npm install
            </li>
            <li>
              Add iOS -
              <small>npx cap add ios</small>
            </li>
            <li>
              Build && start app
            </li>
            <li>
              Open Dev tools
            </li>
            <li>
              Click the X icon to set isEditing to TRUE
            </li>
            <li>
              Web browser should crash
            </li>
          </ol>
        </div>
        <div v-if="isEditing">
          <GMapAutocomplete
            class="w-full flex outline-none tz-standard-input border"
            @place_changed="handlePlaceChanged"
          />
        </div>
        <div
          v-show="!isEditing"
          class="flex"
        >
          <div
            class="
          tz-standard-input
          border
          flex
          justify-between
          items-center
      "
          >
        <span style="">
          {{ formattedAddress }}
        </span>
            <ion-button
              color="gray"
              fill="clear"
              size="small"
              aria-label="clear"
              class="input-clear-icon custom-clear-button"
              @click="setIsEditing(true)"
            >
              <ion-icon :icon="closeCircle" />
            </ion-button>
          </div>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { closeCircle } from 'ionicons/icons/'
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonIcon, IonButton } from '@ionic/vue';
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'TabPageOne',
  components:{ IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonIcon, IonButton },
  data: () => ({
    closeCircle,
    isEditing: false,
    formattedAddress: '123 fake st Beverly Hills, CA 90210'
  }),
  methods: {
    handlePlaceChanged(place: any) {
      console.log('my place ', place)
      setTimeout(() => {
        this.setIsEditing(false)
      }, 2000)
    },
    setIsEditing(isEditing: boolean) {
      this.isEditing = isEditing
    }
  }
})
</script>
<style>
.w-full{
  width: 100%;
}
.flex {
  display: flex;
}
.justify-between {
  justify-content: space-between;
}
.outline-none {
  outline: none;
}
.border {
  border-width: 1px;
  border-style: solid;
  border-color: #E2E8F0;
}
.tz-standard-input {
  background-color:#fff;
  display: inline-flex;
  flex-grow:1;
  padding: 12px 8px;
  color: #1a1a1a;
  align-items: center;
}
</style>