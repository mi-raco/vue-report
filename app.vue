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

const topics = [
        {
          overview: "Kyrone's collapse",
          learnerGoal: 'Give a concise hand-off using TeamSTEPPS tool SBAR',
          learnerResult: '[Success / Needs practice]',
          resultsBreakdown: [
            {
              title: 'Use of SBAR',
              description: '[Did / did not follow SBAR, as identified by LLM-AI]'
            },
            {
              title: 'Hand-off Completeness',
              description: '[Optimal, intermediate, or poor, as identified by AI]'
            },
            {
              title: 'Articulation (word count)',
              description: '[Optimal / Too short / Too long]'
            },
          ]
        },
        // Add more topics as needed...
      ]
</script>

<template>
  <v-container>
    <v-row>
      <v-col>
          <h1>TeamSTEPPS Simulation Report</h1>
          <p>URL is: {{ url }}</p>
          <p>Path is: {{ id }}</p>
          <p>Secret data is: {{ secretData }}</p>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <v-card>
          <v-card-title>
            Learner Details
          </v-card-title>

          <v-card-text>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>
                  Student name/no: [Learner Identifier]
                </v-list-item-title>
                <v-list-item-subtitle>
                  Date: [Date of module completion]
                </v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <v-card color="primary">
          <v-card-title color="primary">
            Overview of Results
          </v-card-title>

          <v-card-text>
            <div>Overall Score: [Score]/100</div>
            <div>TeamSTEPPS Badges: [Badges Earned]</div>
            <v-divider></v-divider>
            <!-- Loop through topics and display results -->
            <div v-for="(result, index) in topics" :key="index">
              <h3>Topic {{ index + 1 }}: {{ result.overview }}</h3>
              <div>Learner Goal: {{ result.learnerGoal }}</div>
              <div>Learner Result: {{ result.learnerResult }}</div>
              <!-- Results Breakdown -->
              <div v-for="(detail, detailIndex) in result.resultsBreakdown" :key="detailIndex">
                <h4>{{ detail.title }}</h4>
                <p>{{ detail.description }}</p>
              </div>
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>