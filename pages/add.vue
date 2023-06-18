<template>
  <MainLayout>
    <div id="AddressPage" class="mt-4 max-w-[500px] mx-auto px-2">
      <div class="mx-auto bg-white rounded-lg p-3">
        <div class="text-xl text-bold mb-2">Add a product</div>
        <form @submit.prevent="submit()">
          <TextInput
            class="w-full"
            placeholder="Title"
            v-model:input="title"
            inputType="text"
            :error="error && error.type == 'title' ? error.message : ''"
          />

          <TextInput
            class="w-full mt-2"
            placeholder="Genre"
            v-model:input="genre"
            inputType="text"
            :error="error && error.type == 'genre' ? error.message : ''"
          />

          <TextInput
            class="w-full mt-2"
            placeholder="Image Url"
            v-model:input="imageUrl"
            inputType="text"
            :error="error && error.type == 'imageUrl' ? error.message : ''"
          />

          <TextInput
            class="w-full mt-2"
            placeholder="Price"
            v-model:input="price"
            inputType="text"
            :error="error && error.type == 'price' ? error.message : ''"
          />

          <TextArea
            class="w-full mt-2"
            placeholder="Description"
            v-model:input="description"
            inputType="text"
            :error="error && error.type == 'description' ? error.message : ''"
          />

          <button
            :disabled="isWorking"
            type="submit"
            class="mt-6 bg-gradient-to-r from-[#c55ffc] to-[#7954a1] w-full text-white text-[21px] font-semibold p-1.5 rounded-full"
          >
            <div v-if="!isWorking">Add an Item</div>
            <Icon v-else name="eos-icons:loading" size="25" class="mr-2" />
          </button>
        </form>
      </div>
    </div>
  </MainLayout>
</template>

<script setup>
import MainLayout from '~/layouts/MainLayout.vue';

const title = ref(null);
const genre = ref(null);
const imageUrl = ref(null);
const description = ref(null);
const price = ref(null);
const error = ref(null);
const isWorking = ref(false);

const submit = async () => {
  isWorking.value = true;
  error.value = '';
  if (!title.value) {
    error.value = {
      type: 'title',
      message: 'A title is required',
    };
  } else if (!genre.value) {
    error.value = {
      type: 'genre',
      message: 'A genre is required',
    };
  } else if (!description.value) {
    error.value = {
      type: 'description',
      message: 'A description is required',
    };
  } else if (!imageUrl.value) {
    error.value = {
      type: 'imageUrl',
      message: 'A url of an image is required',
    };
  } else if (!price.value) {
    error.value = {
      type: 'price',
      message: 'A price is required',
    };
  }
  if (error.value) {
    isWorking.value = false;
    return;
  }

  await useFetch(`/api/prisma/add-product`, {
    method: 'POST',
    body: {
      title: title.value,
      genre: genre.value,
      url: imageUrl.value,
      description: description.value,
      price: Number(price.value * 100),
    },
  });
  isWorking.value = false;
  return navigateTo('/');
};
</script>