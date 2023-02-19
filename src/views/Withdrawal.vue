<template>
  <div>
    <b-row>
      <b-col md="8">
        <h4 class="heading-users m-0">USUARIOS PIDIENDO RETIRAR SU TOKEN</h4>
      </b-col>
    </b-row>
    <b-card no-body>
      <b-tabs card>
        <b-tab
          no-body
          title="Faltan Procesar"
          @click.self="getWithdrawalList('processing')"
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
                  padding-right: 3px;"  @click.stop="filteredWithdrawalsList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchWithdrawl"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredWithdrawalsList"
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
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">cantidade</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(withdrawal, i) in filteredWithdrawalsList()"
                      :key="i"
                      @click="handleOnCheck(withdrawal.withdrawal_id), openUserData(withdrawal.withdrawal_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="withdrawal.withdrawal_id"
                            :checked="selectedWithdrawalsList.includes(withdrawal.withdrawal_id)"
                          />
                        </div>
                      </td>
                      <td></td>
                      <td class="c-table__cell">
                        {{ withdrawal.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ withdrawal.amount }}</td>
                      <td class="c-table__cell">{{ withdrawal.status }}</td>
                      <td class="c-table__cell"></td>
                      <td></td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab
          no-body
          title="Procesados"
          @click.self="getWithdrawalList('successful')"
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
                  padding-right: 3px;"  @click.stop="filteredWithdrawalsList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchWithdrawl"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredWithdrawalsList"
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
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">cantidade</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(withdrawal, i) in filteredWithdrawalsList()"
                      :key="i"
                      @click="handleOnCheck(withdrawal.withdrawal_id), openUserData(withdrawal.withdrawal_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="withdrawal.withdrawal_id"
                            :checked="selectedWithdrawalsList.includes(withdrawal.withdrawal_id)"
                          />
                        </div>
                      </td>
                      <td></td>
                      <td class="c-table__cell">
                        {{ withdrawal.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ withdrawal.amount }}</td>
                      <td class="c-table__cell">{{ withdrawal.status }}</td>
                      <td class="c-table__cell"></td>
                      <td></td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </b-col>
          </b-row>
        </b-tab>
        <b-tab no-body title="Negados" @click.self="getWithdrawalList('denied')">
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
                  padding-right: 3px;"  @click.stop="filteredWithdrawalsList"> 
                  <span
                  class="fa fa-search form-control-feedback1234" style="position:relative; top:0; left:0px !important"
                ></span>
              </span>
                <input
                  v-model="searchWithdrawl"
                  type="text"
                  class="form-control"
                  placeholder="Search Contact"
                  @click.stop="filteredWithdrawalsList"
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
                      <th></th>
                      <th class="c-table__col-label">Propietario</th>
                      <th class="c-table__col-label">cantidade</th>
                      <th class="c-table__col-label">Estatus</th>
                    </tr>
                  </thead>
                  <tbody class="c-table__body">
                    <tr
                      v-for="(withdrawal, i) in filteredWithdrawalsList()"
                      :key="i"
                      @click="handleOnCheck(withdrawal.withdrawal_id), openUserData(withdrawal.withdrawal_id)"
                    >
                      <td class="c-table__cell">
                        <div class="form-check">
                          <input
                            class="form-check-input custom-checkbox"
                            type="checkbox"
                            :value="withdrawal.withdrawal_id"
                            :checked="selectedWithdrawalsList.includes(withdrawal.withdrawal_id)"
                          />
                        </div>
                      </td>
                      <td></td>
                      <td class="c-table__cell">
                        {{ withdrawal.nombre_usuario }}
                      </td>
                      <td class="c-table__cell">{{ withdrawal.amount }}</td>
                      <td class="c-table__cell">{{ withdrawal.status }}</td>
                      <td class="c-table__cell"></td>
                      <td></td>
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
      @close="closeUserData(), clearSelectedWithdrawalsList()"
      @modal-delete="openModalDelete"
      :content="withdrawalData"
      :withdrawalId="withdrawalId"
      :activeTab="activeTab"
    />
    <!--    delete modal-->
    <ModalDelete
      v-show="modalDeleteVisible"
      @remove="removeWithdrawalFromArray"
      @close="closeModalDelete"
      :withdrawalId="withdrawalId"
    />
  </div>
</template>
<script setup>
import { ref } from 'vue'
import { useStore } from 'vuex'
import UserDataModal from '@/components/withdrawal/UserDataModal.vue'
import ModalDelete from '@/components/withdrawal/ModalDelete.vue'

let users = ref([
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
const store = useStore()
const userDataVisible = ref(false)
const modalDeleteVisible = ref(false)
let withdrawalList = ref(0)
let searchWithdrawl = ref('')
let withdrawalData = ref({})
let activeTab = ref('')

function getWithdrawalList(status) {
  if (event) {
    activeTab.value = event.target.textContent;
  } else {
    activeTab.value = 'Faltan Procesar';
  }
  withdrawalList.value = [];
  searchWithdrawl.value = '';
  const data = JSON.stringify({ status: status })
  store.dispatch('getWithdrawlList', data).then((response) => {
    if (response.content) {
      withdrawalList.value = response.content
    }
  })
}

getWithdrawalList('processing')

function getWithdrawlByRequester(type) {
  let payload = JSON.stringify({
    username: searchWithdrawl.value,
  })
  store.dispatch('getWithdrawlByRequester', payload).then((response) => {
    if (response.status) {
      this.withdrawalList =
        response.content.length > 0 &&
        response.content.filter((e) => e.status === type)
    }
  })
}

function openUserData(withdrawalId) {
  userDataVisible.value = true
  if (withdrawalId) {
    const data = JSON.stringify({ withdrawal_id: withdrawalId })
    store.dispatch('getWithdrawlInfo', data).then((response) => {
      if (response.content) {
        withdrawalData.value = response.content
      }
    })
  }
}

function closeUserData() {
  userDataVisible.value = false
}

function openModalDelete() {
  modalDeleteVisible.value = true
}

function closeModalDelete(closeAll) {
  modalDeleteVisible.value = false

  if (closeAll) closeUserData()
}
</script>

<script>
import Swal from 'sweetalert2'
export default {
  name: 'Withdrawal',
  data: function () {
    return {
      withdrawalId: '',
      withdrawalData: {},
      selectedWithdrawalsList: [],
    }
  },
  methods: {
    handleOnCheck(withdrawalId) {
      if (!this.selectedWithdrawalsList.includes(withdrawalId)) {
        this.withdrawalId = withdrawalId;
        this.selectedWithdrawalsList.push(withdrawalId);
      } else {
        const withdrawalIndex = this.selectedWithdrawalsList.findIndex(el => el === withdrawalId);
        if (withdrawalIndex > -1) {
          this.withdrawalId = '';
          this.selectedWithdrawalsList.splice(withdrawalIndex, 1);
        }
      }
    },
    filteredWithdrawalsList() {
      if (this.searchWithdrawl) {
        return this.withdrawalList.filter(withdrawal => withdrawal.nombre_usuario.startsWith(this.searchWithdrawl));
      }
      return this.withdrawalList;
    },
    removeWithdrawalFromArray(withdrawalId) {
      const withdrawalIndex = this.withdrawalList.findIndex(({ withdrawal_id }) => withdrawal_id === withdrawalId);
      if (withdrawalIndex > -1) {
        this.withdrawalList.splice(withdrawalIndex, 1);
        this.clearSelectedWithdrawalsList();
      }
    },
    clearSelectedWithdrawalsList() {
      this.selectedWithdrawalsList = [];
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
