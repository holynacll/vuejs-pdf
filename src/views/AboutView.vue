<!-- <template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template> -->
<template>
  <div
    class="mx-auto p-8 bg-gradient-to-br from-blue-200 via-purple-300 to-pink-400 h-screen flex flex-col items-center justify-center"
  >
    <h1 class="text-5xl font-bold mb-4 text-black">AI Contracts</h1>
    <p class="text-lg font-semibold text-gray-800 mb-8">
      Resuma as Principais Informações de Qualquer Contrato Instantaneamente
    </p>

    <div class="bg-white p-8 rounded-lg shadow-lg w-96 flex flex-col items-center">
      <div
        class="w-64 h-48 bg-blue-50 border-gray-400 rounded-lg flex flex-col items-center justify-center mb-4 cursor-pointer"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          strokeWidth="{1.5}"
          stroke="currentColor"
          class="size-10 text-2xl font-bold antialiased text-white mb-2 bg-blue-600 rounded-full p-2"
        >
          <path strokeLinecap="round" strokeLinejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
        </svg>

        <p class="text-gray-700 font-semibold antialiased" for="fileInput">
          Solte seu arquivo aqui
        </p>
        <input
          type="file"
          id="fileInput"
          ref="fileInput"
          style="display: none"
          @change="uploadFile"
          accept=".pdf"
        />
      </div>

      <div class="flex items-center">
        <p class="text-gray-600 font-semibold mr-2">Seu documento está online?</p>
        <a href="#" class="text-gray-800 font-bold underline">Link Upload</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  methods: {
    uploadFile() {
      const fileInput = this.$refs.fileInput
      const file = fileInput.files[0]

      if (!file) {
        return
      }

      const formData = new FormData()
      formData.append('file', file)

      const url = 'http://localhost:8000/analyze-contract'
      axios
        .post(url, formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        })
        .then((response) => {
          // Sucesso! Faça algo com a resposta da API, como exibir uma mensagem de sucesso
          console.log(response.data)
        })
        .catch((error) => {
          // Trate erros de upload aqui, como exibir uma mensagem de erro
          console.error(error)
        })
    }
  }
}
</script>
