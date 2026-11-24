<script setup>
import { ref, computed } from 'vue'

const searchQuery = ref('')
const selectedLevel = ref('All')

const universities = ref([
  {
    id: 1,
    name: 'Stanford University',
    location: 'Stanford, CA, USA',
    level: 'Graduate & PhD',
    field: 'Computer Science & AI',
    tuition: '$58,700 / year',
    deadline: 'Dec 15, 2026',
    description: 'World-renowned hub for tech innovation, AI research, and venture incubation with top-tier graduate placement.',
    imageBg: 'linear-gradient(135deg, #8c1515 0%, #b83a3a 100%)'
  },
  {
    id: 2,
    name: 'Massachusetts Institute of Technology (MIT)',
    location: 'Cambridge, MA, USA',
    level: 'Graduate & PhD',
    field: 'Engineering & Robotics',
    tuition: '$60,150 / year',
    deadline: 'Jan 05, 2027',
    description: 'Leading global institution advancing pioneering research in quantum computing, robotics, and advanced engineering.',
    imageBg: 'linear-gradient(135deg, #a31f34 0%, #d32f46 100%)'
  },
  {
    id: 3,
    name: 'University of Oxford',
    location: 'Oxford, United Kingdom',
    level: 'Graduate & Master',
    field: 'Humanities & Social Sciences',
    tuition: '£31,200 / year',
    deadline: 'Jan 22, 2027',
    description: 'Historic academic excellence offering rigorous collegiate postgraduate degrees with world-class libraries and mentorship.',
    imageBg: 'linear-gradient(135deg, #002147 0%, #003366 100%)'
  },
  {
    id: 4,
    name: 'ETH Zurich',
    location: 'Zurich, Switzerland',
    level: 'Graduate & Master',
    field: 'Engineering & Sciences',
    tuition: 'CHF 1,460 / semester',
    deadline: 'Dec 15, 2026',
    description: 'Top European science and technology university known for Nobel laureates, rigorous curricula, and central European location.',
    imageBg: 'linear-gradient(135deg, #1f4788 0%, #336699 100%)'
  },
  {
    id: 5,
    name: 'National University of Singapore (NUS)',
    location: 'Singapore',
    level: 'Undergraduate & Graduate',
    field: 'Business & Analytics',
    tuition: '$38,500 / year',
    deadline: 'Mar 01, 2027',
    description: 'Asia’s top-ranking global university providing cutting-edge business analytics and multidisciplinary undergraduate programs.',
    imageBg: 'linear-gradient(135deg, #ef7c00 0%, #f7931e 100%)'
  },
  {
    id: 6,
    name: 'University of California, Berkeley',
    location: 'Berkeley, CA, USA',
    level: 'Graduate & PhD',
    field: 'Data Science & Public Policy',
    tuition: '$54,200 / year',
    deadline: 'Dec 01, 2026',
    description: 'Premier public research institution fostering groundbreaking public policy, data science, and biotechnology breakthroughs.',
    imageBg: 'linear-gradient(135deg, #003262 0%, #fdb515 100%)'
  }
])

const filteredUniversities = computed(() => {
  return universities.value.filter(uni => {
    const matchesSearch = uni.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                          uni.field.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                          uni.location.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesLevel = selectedLevel.value === 'All' || uni.level.includes(selectedLevel.value)
    return matchesSearch && matchesLevel
  })
})

const emit = defineEmits(['selectUni'])
</script>

<template>
  <section id="universities">
    <div class="container">
      <div class="section-header">
        <h2>Top Universities & Programs</h2>
        <p>Explore world-class institutions, tuition estimates, admission deadlines, and research focus areas.</p>
      </div>

      <div class="filter-bar">
        <input 
          type="text" 
          v-model="searchQuery" 
          placeholder="Search universities or fields of study..." 
          class="search-input"
        />
        <select v-model="selectedLevel" class="select-input">
          <option value="All">All Degree Levels</option>
          <option value="Undergraduate">Undergraduate</option>
          <option value="Graduate">Graduate & Master</option>
          <option value="PhD">PhD / Doctorate</option>
        </select>
      </div>

      <div class="filter-chips">
        <button 
          v-for="level in ['All', 'Undergraduate', 'Graduate', 'PhD']" 
          :key="level"
          class="chip"
          :class="{ active: selectedLevel === level }"
          @click="selectedLevel = level"
        >
          {{ level }}
        </button>
      </div>

      <div class="grid">
        <div v-for="uni in filteredUniversities" :key="uni.id" class="card">
          <div>
            <div class="uni-header" :style="{ background: uni.imageBg }">
              <span class="uni-badge">{{ uni.level }}</span>
              <h3>{{ uni.name }}</h3>
              <p class="uni-location">📍 {{ uni.location }}</p>
            </div>
            <div class="uni-body">
              <p class="uni-desc">{{ uni.description }}</p>
              <div class="uni-meta">
                <span><strong>Field:</strong> {{ uni.field }}</span>
                <span><strong>Tuition:</strong> {{ uni.tuition }}</span>
                <span><strong>Deadline:</strong> {{ uni.deadline }}</span>
              </div>
            </div>
          </div>
          <div class="uni-footer">
            <button class="btn" @click="$emit('selectUni', uni)">Inquire & Connect</button>
          </div>
        </div>
      </div>

      <div v-if="filteredUniversities.length === 0" class="no-results">
        <p>No universities found matching your search. Try adjusting your filters.</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.uni-header {
  padding: 20px;
  border-radius: 8px;
  color: white;
  margin-bottom: 16px;
  min-height: 120px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

.uni-badge {
  align-self: flex-start;
  background: rgba(255, 255, 255, 0.2);
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 8px;
  backdrop-filter: blur(4px);
}

.uni-header h3 {
  color: white;
  margin: 0 0 4px 0;
  font-size: 20px;
}

.uni-location {
  font-size: 13px;
  opacity: 0.9;
  margin: 0;
}

.uni-desc {
  font-size: 14px;
  color: var(--text);
  margin-bottom: 16px;
  line-height: 1.5;
}

.uni-meta {
  display: flex;
  flex-direction: column;
  gap: 6px;
  font-size: 13px;
  background: var(--bg);
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 20px;
  border: 1px solid var(--border);
}

.uni-footer {
  display: flex;
  justify-content: flex-end;
}

.no-results {
  text-align: center;
  padding: 48px;
  color: var(--text);
  font-size: 16px;
}
</style>
