<template>
  <div>
    <h2 class="text-center mt-5 mb-5">List of Student Pamulang University</h2>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-lg-10">
          <div class="card">
            <div
              class="card-header bg-white d-flex justify-content-between align-items-center"
            >
              <h5>Table students</h5>
              <router-link to="/create" class="btn btn-primary"
                ><span class="fw-bold">+</span> Add new students</router-link
              >
            </div>
            <div class="card-body">
              <div
                v-if="loading"
                class="w-100 d-flex justify-content-center align-items-center"
              >
                <img src="@/assets/img/infinity.svg" alt="" width="100" />
              </div>
              <table class="table" v-else>
                <thead>
                  <tr>
                    <th scope="col">#</th>
                    <th scope="col">Name</th>
                    <th scope="col">NIM</th>
                    <th scope="col">Date of Birth</th>
                    <th scope="col">Address</th>
                    <th scope="col">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(ls, index) in listStudent.data" :key="ls.id">
                    <th scope="row">{{ index + 1 }}</th>
                    <td>{{ ls.name }}</td>
                    <td>{{ ls.nim }}</td>
                    <td>{{ ls.date_birth }}</td>
                    <td>{{ ls.address }}</td>
                    <td>
                      <router-link
                        :to="`/edit/${ls.id}`"
                        class="btn btn-info text-white"
                        >Edit</router-link
                      >
                      <button
                        to=""
                        class="btn btn-danger mx-2"
                        @click="destroy(ls.id, index)"
                      >
                        delete
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive, onMounted } from "vue";

let listStudent = ref([]);
let loading = ref(true);

const destroy = (id, index) => {
  axios
    .delete(`http://127.0.0.1:8000/api/mahasiswa/${id}`)
    .then(function (response) {
      listStudent.value.data.splice(index, 1);
    })
    .catch(function (error) {
      // handle error
      console.log(error);
    });
};
onMounted(() => {
  axios
    .get("http://127.0.0.1:8000/api/mahasiswa")
    .then(function (response) {
      listStudent.value = response.data;
    })
    .catch(function (error) {
      // handle error
      console.log(error.response.data);
    })
    .finally(function () {
      // always executed
      loading.value = false;
    });
});
</script>
