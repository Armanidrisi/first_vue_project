<template>
  <section class="vh-100" style="background-color: #f4f5f7">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-lg-6 mb-4 mb-lg-0">
          <div class="card mb-3" style="border-radius: 0.5rem">
            <div class="row g-0">
              <div
                class="col-md-4 gradient-custom text-center text-white"
                :style="{
                  borderTopLeftRadius: '0.5rem',
                  borderBottomLeftRadius: '0.5rem',
                }"
              >
                <img
                  :src="user.picture?.large"
                  alt="Avatar"
                  class="img-fluid my-5"
                  :style="{
                    width: '130px',
                    borderRadius: '50%',
                    border: '3px solid #f6d365',
                  }"
                />
                <h5>{{ user.name?.first }} {{ user.name?.last }}</h5>
                <p>@{{ user.login?.username }}</p>
              </div>
              <div class="col-md-8">
                <div class="card-body p-4">
                  <h6>Information</h6>
                  <hr class="mt-0 mb-4" />
                  <div class="row pt-1">
                    <div class="col-6 mb-3">
                      <h6>Email</h6>
                      <p class="text-muted">{{ user.email }}</p>
                    </div>
                    <div class="col-6 mb-3">
                      <h6>Phone</h6>
                      <p class="text-muted">{{ user.phone }}</p>
                    </div>
                  </div>
                  <h6>Address</h6>
                  <hr class="mt-0 mb-4" />
                  <div class="row pt-1">
                    <div class="col-6 mb-3">
                      <p class="text-muted">
                        {{ user.location?.street?.number }}
                        {{ user.location?.street?.name }},
                        {{ user.location?.city }}, {{ user.location?.state }},
                        {{ user.location?.country }},
                        {{ user.location?.postcode }}
                      </p>
                    </div>
                  </div>
                  <button
                    @click="fetchPosts"
                    type="button"
                    class="btn btn-primary"
                  >
                    Random
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const user = ref({});

const fetchPosts = async () => {
  try {
    const response = await fetch('https://randomuser.me/api');
    const data = await response.json();
    user.value = data.results[0];
  } catch (error) {
    alert('There was an error occurred, please check your network connection');
  }
};

onMounted(fetchPosts);
</script>
