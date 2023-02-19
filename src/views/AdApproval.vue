<template>
  <div>
    <b-row>
      <b-col md="8">
        <h4 class="heading-users m-0">
          USUARIOS PIDIENDO APROBACIÓN DE SUS ANUNCIOS
        </h4>
      </b-col>
    </b-row>
    <b-card no-body>
      <b-tabs card>
        <b-tab no-body title="Faltan Procesar" @click.self="getAdsList('in review')">
          <b-row class="mt-5">
            <b-col md="10" class="d-inline-flex align-items-center">
              <!-- <div class="form-check search-cb">
                <input
                  class="form-check-input custom-checkbox"
                  type="checkbox"
                  value=""
                />
              </div> -->
              <!-- Actual search box -->
              <div
                class="form-group has-search d-inline-block position-relative"
              >
              <span style="border:1px solid #b3b0b0;border-radius: 5px;
                  padding-left: 3px;
                  position: absolute;
                  margin-top: 6px;
                  margin-left: 10px;
                  height: auto;
                  margin-bottom: 10px;
                  padding-right: 3px;"  @click.stop="filteredAdvertisesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchAdvertise"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredAdvertisesList"
                />
              </div>
            </b-col>
          </b-row>
          <b-row class="mt-4">
            <b-col md="12">
              <div class="wrapper">
                <table class="c-table">
                  <thead class="c-table__header">
                    <tr>
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">Publicar enlace</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(ad, i) in filteredAdvertisesList()"
                      :key="i"
                      @click="handleOnCheck(ad.advertise_id), openUserData(ad.advertise_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="ad.advertise_id"
                            :checked="selectedAdsList.includes(ad.advertise_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">{{ ad.nombre_usuario }}</td>
                      <td class="c-table__cell word-break">{{ ad.post_link }}</td>
                      <td class="c-table__cell">{{ ad.status }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab no-body title="Procesados" @click.self="getAdsList('approved')">
          <b-row class="mt-5">
            <b-col md="10" class="d-inline-flex align-items-center">
              <!-- <div class="form-check search-cb">
                <input
                  class="form-check-input custom-checkbox"
                  type="checkbox"
                />
              </div> -->
              <!-- Actual search box -->
              <div
                class="form-group has-search d-inline-block position-relative"
              >
              <span style="border:1px solid #b3b0b0;border-radius: 5px;
                  padding-left: 3px;
                  position: absolute;
                  margin-top: 6px;
                  margin-left: 10px;
                  height: auto;
                  margin-bottom: 10px;
                  padding-right: 3px;"  @click.stop="filteredAdvertisesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchAdvertise"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredAdvertisesList"
                />
              </div>
            </b-col>
          </b-row>
          <b-row class="mt-4">
            <b-col md="12">
              <div class="wrapper">
                <table class="c-table">
                  <thead class="c-table__header">
                    <tr>
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">Publicar enlace</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(ad, i) in filteredAdvertisesList()"
                      :key="i"
                      @click="handleOnCheck(ad.advertise_id), openUserData(ad.advertise_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="ad.advertise_id"
                            :checked="selectedAdsList.includes(ad.advertise_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">{{ ad.nombre_usuario }}</td>
                      <td class="c-table__cell word-break">{{ ad.post_link }}</td>
                      <td class="c-table__cell">{{ ad.status }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab no-body title="Negados" @click.self="getAdsList('denied')">
          <b-row class="mt-5">
            <b-col md="10" class="d-inline-flex align-items-center">
              <!-- <div class="form-check search-cb">
                <input
                  class="form-check-input custom-checkbox"
                  type="checkbox"
                />
              </div> -->
              <!-- Actual search box -->
              <div
                class="form-group has-search d-inline-block position-relative"
              >
              <span style="border:1px solid #b3b0b0;border-radius: 5px;
                  padding-left: 3px;
                  position: absolute;
                  margin-top: 6px;
                  margin-left: 10px;
                  height: auto;
                  margin-bottom: 10px;
                  padding-right: 3px;"  @click.stop="filteredAdvertisesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchAdvertise"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredAdvertisesList"
                />
              </div>
            </b-col>
          </b-row>
          <b-row class="mt-4">
            <b-col md="12">
              <div class="wrapper">
                <table class="c-table">
                  <thead class="c-table__header">
                    <tr>
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">Publicar enlace</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(ad, i) in filteredAdvertisesList()"
                      :key="i"
                      @click="handleOnCheck(ad.advertise_id), openUserData(ad.advertise_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="ad.advertise_id"
                            :checked="selectedAdsList.includes(ad.advertise_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">{{ ad.nombre_usuario }}</td>
                      <td class="c-table__cell word-break">{{ ad.post_link }}</td>
                      <td class="c-table__cell">{{ ad.status }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
      </b-tabs>
    </b-card>

    <!-- modal 18-->
    <UserDataModal
      v-show="userDataVisible"
      @close="closeUserData(), clearSelectedAdsList()"
      @show-confirm="openConfirmModal"
      :content="adsData"
      :advertiseId="adsId"
      :activeTab="activeTab"
    />

    <!--    confirm modal-->
    <ConfirmModal
      v-show="confirmModalVisible"
      @remove="removeAdvertisementFromArray"
      @close="closeConfirmModal"
      :advertiseId="adsId"
    />
  </div>
</template>
<script setup>
import { ref, watch } from 'vue'
import { useStore } from 'vuex'
import UserDataModal from '@/components/adApproval/UserDataModal.vue'
import ConfirmModal from '@/components/adApproval/ConfirmModal.vue'
const store = useStore()
let adsList = ref(0)
let searchAdvertise = ref('')
let adsDetails = ref(null)
let adsData = ref({})
let activeTab = ref('')

function getAdsList(status) {
  if (event) {
    activeTab.value = event.target.textContent;
  } else {
    activeTab.value = 'Faltan Procesar';
  }
  adsList.value = [];
  searchAdvertise.value = '';
  const data = JSON.stringify({ status: status })
  store.dispatch('getAdvertisesList', data).then((response) => {
    if (response.content) {
      adsList.value = response.content
    }
  })
}
getAdsList('in review')

const userDataVisible = ref(false)
const confirmModalVisible = ref(false)

function getAdvertiseByRequester(type) {
  let payload = JSON.stringify({
    username: searchAdvertise.value,
  })
  store.dispatch('getAdvertiseByRequester', payload).then((response) => {
    if (response.status) {
      this.adsList =
        response.content.length > 0 &&
        response.content.filter((e) => e.status === type)
    }
  })
}
function openUserData(adsId) {
  userDataVisible.value = true

  if (adsId) {
    const data = JSON.stringify({ advertise_id: adsId })
    store.dispatch('getAdvertiseInfo', data).then((response) => {
      if (response.content) {
        adsData.value = response.content
      }
    })
  }
}

function closeUserData() {
  userDataVisible.value = false
}

function openConfirmModal() {
  confirmModalVisible.value = true
}

function closeConfirmModal(closeAll) {
  confirmModalVisible.value = false

  if (closeAll) closeUserData()
}
</script>

<script>
import Swal from 'sweetalert2'
export default {
  name: 'Ad',
  data: function () {
    return {
      adsId: '',
      adsData: {},
      selectedAdsList: []
    }
  },
  methods: {
    handleOnCheck(advertisementId) {
      if (!this.selectedAdsList.includes(advertisementId)) {
        this.adsId = advertisementId;
        this.selectedAdsList.push(advertisementId);
      } else {
        const adIndex = this.selectedAdsList.findIndex(el => el === advertisementId);
        if (adIndex > -1) {
          this.adsId = '';
          this.selectedAdsList.splice(adIndex, 1);
        }
      }
    },
    filteredAdvertisesList() {
      if (this.searchAdvertise) {
        return this.adsList.filter(ad => ad.nombre_usuario.startsWith(this.searchAdvertise));
      }
      return this.adsList;
    },
    removeAdvertisementFromArray(advertisementId) {
      const adIndex = this.adsList.findIndex(({ advertise_id }) => advertise_id === advertisementId);
      if (adIndex > -1) {
        this.adsList.splice(adIndex, 1);
        this.clearSelectedAdsList();
      }
    },
    clearSelectedAdsList() {
      this.selectedAdsList = [];
    }
  },
}
</script>
<style lang="scss">
.head {
  font-weight: 600;
  font-size: 16px;
  color: #323c43;
}
.sm-btn-c {
  width: 120px;
  padding: unset;
}
.form-control-feedback12 {
  left: 13px !important;
  position: absolute;
}
.form-control-feedback123 {
  left: 13px !important;
  position: absolute;
  top: 19px;
}
.form-control-feedback1234 {
  left: 13px !important;
  position: absolute;
  top: 11px;
}
.word-break {
  word-break: break-word;
}
</style>
