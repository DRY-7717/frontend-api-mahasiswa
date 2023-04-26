<template>
  <div class="container">
    <h2 class="text-center mt-5 mb-5">Create Data Students</h2>

    <div class="row justify-content-center">
      <div class="col-lg-10">
        <div class="card">
          <div class="card-header bg-white">
            <router-link to="/" class="btn btn-primary"
              >Back to home</router-link
            >
          </div>
          <div class="card-body">
            <form @submit.prevent="createData">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Name</label>
                <input
                  type="text"
                  class="form-control"
                  :class="validation.name ? 'is-invalid' : false"
                  id="name"
                  name="name"
                  v-model="students.name"
                />
                <div class="invalid-feedback" v-if="validation.name">
                  {{ validation.name[0] }}
                </div>
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">NIM</label>
                <input
                  type="number"
                  :class="validation.nim ? 'is-invalid' : false"
                  class="form-control"
                  id="nim"
                  name="nim"
                  v-model="students.nim"
                />
                <div class="invalid-feedback" v-if="validation.nim">
                  {{ validation.nim[0] }}
                </div>
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Date of Birth</label
                >
                <input
                  type="date"
                  :class="validation.date_birth ? 'is-invalid' : false"
                  class="form-control"
                  id="date_birth"
                  name="date_birth"
                  v-model="students.date_birth"
                />
                <div class="invalid-feedback" v-if="validation.date_birth">
                  {{ validation.date_birth[0] }}
                </div>
              </div>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"
                  >Address</label
                >
                <input
                  type="text"
                  class="form-control"
                  :class="validation.address ? 'is-invalid' : false"
                  id="address"
                  name="address"
                  v-model="students.address"
                />
                <div class="invalid-feedback" v-if="validation.address">
                  {{ validation.address[0] }}
                </div>
              </div>

              <button type="submit" class="btn btn-primary">Submit</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref, onMounted } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

let validation = ref([]);

let students = reactive({
  name: "",
  nim: "",
  date_birth: "",
  address: "",
});

const createData = () => {
  axios
    .post("http://127.0.0.1:8000/api/mahasiswa", students)
    .then(function (response) {
      router.push("/");
    })
    .catch(function (error) {
      // handle error
      validation.value = error.response.data.errors;
    });
};
</script>
