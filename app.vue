<script setup lang="ts">
import { ref } from 'vue'
import { findOne } from "~/api/mongoDataAPI" 

const url = useRequestURL()
const id = url.pathname.replace('/', '')
const secretData = ref(null)

const response = await findOne(
  "threads", 
  {"_id": {"$oid": id}}
)
secretData.value = response.document.data

</script>

<template>
  <p>URL is: {{ url }}</p>
  <p>Path is: {{ id }}</p>
  <p>Secret data is: {{ secretData }}</p>
</template>