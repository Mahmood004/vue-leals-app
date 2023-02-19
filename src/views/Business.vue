<template>
  <div>
    <b-row>
      <b-col md="8">
        <h4 class="heading-users m-0">
          USUARIOS PIDIENDO APROBACIÓN DE SUS NEGOCIOS
        </h4>
      </b-col>
    </b-row>
    <b-card no-body>
      <b-tabs card>
        <b-tab
          no-body
          title="Faltan Procesar"
          @click.self="getBusinessList('in review', $event)"
        >
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
                  padding-right: 3px;"  @click.stop="filteredBusinessesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchBusiness"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredBusinessesList"
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
                      <th class="c-table__col-label" style="width: 200px">
                        Nombre usuario
                      </th>
                      <th class="c-table__col-label">Categoría</th>
                      <th class="c-table__col-label">Nombre del Negocio</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(business, i) in filteredBusinessesList()"
                      :key="i"
                      @click="handleOnCheck(business.business_id), openUserData(business.business_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="business.business_id"
                            :checked="selectedBusinessesList.includes(business.business_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">
                        {{ business.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ business.category }}</td>
                      <td class="c-table__cell">
                        {{ business.business_name }}
                      </td>
                      <td class="c-table__cell">
                        {{ business.business_status }}
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab no-body title="Procesados" @click.self="getBusinessList('approved', $event)">
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
                  padding-right: 3px;"  @click.stop="filteredBusinessesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchBusiness"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredBusinessesList"
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
                      <th class="c-table__col-label" style="width: 200px">
                        Nombre usuario
                      </th>
                      <th class="c-table__col-label">Categoría</th>
                      <th class="c-table__col-label">Nombre del Negocio</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(business, i) in filteredBusinessesList()"
                      :key="i"
                      @click="handleOnCheck(business.business_id), openUserData(business.business_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="business.business_id"
                            :checked="selectedBusinessesList.includes(business.business_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">
                        {{ business.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ business.category }}</td>
                      <td class="c-table__cell">
                        {{ business.business_name }}
                      </td>
                      <td class="c-table__cell">
                        {{ business.business_status }}
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab no-body title="Negados" @click.self="getBusinessList('denied', $event)">
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
                  padding-right: 3px;"  @click.stop="filteredBusinessesList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchBusiness"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredBusinessesList"
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
                      <th class="c-table__col-label" style="width: 200px">
                        Nombre usuario
                      </th>
                      <th class="c-table__col-label">Categoría</th>
                      <th class="c-table__col-label">Nombre del Negocio</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(business, i) in filteredBusinessesList()"
                      :key="i"
                      @click="handleOnCheck(business.business_id), openUserData(business.business_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="business.business_id"
                            :checked="selectedBusinessesList.includes(business.business_id)"
                          />
                        </div>
                      </td>
                      <td class="c-table__cell">
                        {{ business.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ business.category }}</td>
                      <td class="c-table__cell">
                        {{ business.business_name }}
                      </td>
                      <td class="c-table__cell">
                        {{ business.business_status }}
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
      </b-tabs>
    </b-card>

    <!--    modal 18-->
    <UserDataModal
      v-show="userDataVisible"
      @close="closeUserData(), clearSelectedBusinessesList()"
      @show-confirm="openConfirmModal"
      :content="businessData"
      :businessId="businessId"
      :activeTab="activeTab"
    />
    <!--    confirm modal-->
    <ConfirmModal
      v-show="confirmModalVisible"
      @remove="removeBusinessFromArray"
      @close="closeConfirmModal"
      :businessId="businessId"
    />
  </div>
</template>
<script setup>
import { ref } from 'vue'
import { useStore } from 'vuex'
import UserDataModal from '@/components/business/UserDataModal.vue'
import ConfirmModal from '@/components/business/ConfirmModal.vue'
const store = useStore()
const users = ref([
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
  {
    name: 'Alice Blue',
    email: 'aliceblue@example.com',
    amount: '763012721',
    picture: '/img/profile.jpg',
  },
])

let activeTab = ref('')
let searchBusiness = ref('')
let businessList = ref(0)
let businessData = ref({})

function getBusinessList(status, event = null) {
  if (event) {
    activeTab.value = event.target.textContent;
  } else {
    activeTab.value = 'Faltan Procesar';
  }
  businessList.value = [];
  searchBusiness.value = '';
  const data = JSON.stringify({ business_status: status })
  store.dispatch('getBusinessesList', data).then((response) => {
    if (response.content) {
      businessList.value = response.content
    }
  })
}
getBusinessList('in review')

function getBusinessByRequester(type, event) {
  event.stopPropagation();
  if (searchBusiness.value) {
    let payload = JSON.stringify({
      username: searchBusiness.value,
    })
    store.dispatch('getBusinessByRequester', payload).then((response) => {
      if (response.status == true) {
        this.businessList =
          response.content.length > 0 &&
          response.content.filter((e) => e.business_status === type)
      }
    })
  }
}

const userDataVisible = ref(false)
const confirmModalVisible = ref(false)

function openUserData(businessId) {
  userDataVisible.value = true
  if (businessId) {
    const data = JSON.stringify({ business_id: businessId })
    store.dispatch('getBusinessInfo', data).then((response) => {
      if (response.content) {
        businessData.value = response.content
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
  name: 'Business',
  data: function () {
    return {
      businessId: '',
      businessData: {},
      selectedBusinessesList: [],
    }
  },
  methods: {
    handleOnCheck(businessId) {
      if (!this.selectedBusinessesList.includes(businessId)) {
        this.businessId = businessId;
        this.selectedBusinessesList.push(businessId);
      } else {
        const businessIndex = this.selectedBusinessesList.findIndex(el => el === businessId);
        if (businessIndex > -1) {
          this.businessId = '';
          this.selectedBusinessesList.splice(businessIndex, 1);
        }
        
      }
    },
    filteredBusinessesList() {
      if (this.searchBusiness) {
        return this.businessList.filter(business => business.nombre_usuario.startsWith(this.searchBusiness));
      }
      return this.businessList;
    },
    removeBusinessFromArray(businessId) {
      const businessIndex = this.businessList.findIndex(({ business_id }) => business_id === businessId);
      if (businessIndex > -1) {
        this.businessList.splice(businessIndex, 1);
        this.clearSelectedBusinessesList();
      }
    },
    clearSelectedBusinessesList() {
      this.selectedBusinessesList = [];
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
</style>
