<script setup>
import { ref } from 'vue'

const mentors = ref([
  {
    id: 1,
    name: 'Dr. Elena Rostova',
    role: 'PhD Candidate in AI & ML',
    university: 'Stanford University',
    expertise: 'Natural Language Processing, Statement of Purpose (SOP) Review, Fellowship Applications',
    bio: 'Alumna of Oxford University. Helping undergraduate students navigate PhD admissions, research proposals, and fellowship interviews.',
    avatar: '👩‍🎓'
  },
  {
    id: 2,
    name: 'Marcus Chen',
    role: 'MS in Robotics & Control',
    university: 'MIT',
    expertise: 'Robotics Labs, Technical Portfolio, GRE/GMAT Prep',
    bio: 'Passionate about mentoring engineering students on research internships, lab applications, and master’s funding opportunities.',
    avatar: '👨‍🎓'
  },
  {
    id: 3,
    name: 'Aisha Al-Mansoor',
    role: 'DPhil in Economics',
    university: 'University of Oxford',
    expertise: 'Macroeconomics, Academic Writing, Rhodes Scholarship Prep',
    bio: ' Rhodes Scholar mentoring prospective graduate applicants on scholarship essays, interview preparation, and research design.',
    avatar: '👩‍🔬'
  }
])

const emit = defineEmits(['requestMentorship'])
</script>

<template>
  <section id="mentors" style="background: var(--card-bg); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);">
    <div class="container">
      <div class="section-header">
        <h2>Meet Graduate Mentors</h2>
        <p>Connect 1-on-1 with graduate students and PhD candidates who have successfully walked the path you are pursuing.</p>
      </div>

      <div class="grid">
        <div v-for="mentor in mentors" :key="mentor.id" class="card mentor-card">
          <div>
            <div class="mentor-profile">
              <div class="avatar">{{ mentor.avatar }}</div>
              <div>
                <h3>{{ mentor.name }}</h3>
                <p class="mentor-role">{{ mentor.role }}</p>
                <p class="mentor-uni">🏛️ {{ mentor.university }}</p>
              </div>
            </div>
            <p class="mentor-bio">{{ mentor.bio }}</p>
            <div class="mentor-expertise">
              <span class="tag" v-for="exp in mentor.expertise.split(',')" :key="exp">{{ exp.trim() }}</span>
            </div>
          </div>
          <div class="mentor-footer">
            <button class="btn btn-outline" @click="$emit('requestMentorship', mentor)">Request Mentorship</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.mentor-profile {
  display: flex;
  gap: 16px;
  align-items: center;
  margin-bottom: 16px;
}

.avatar {
  font-size: 40px;
  background: var(--bg);
  width: 64px;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  border: 1px solid var(--border);
  flex-shrink: 0;
}

.mentor-profile h3 {
  margin: 0 0 2px 0;
  font-size: 18px;
  color: var(--text-h);
}

.mentor-role {
  font-size: 14px;
  font-weight: 600;
  color: var(--primary);
  margin: 0 0 2px 0;
}

.mentor-uni {
  font-size: 13px;
  color: var(--text);
  margin: 0;
}

.mentor-bio {
  font-size: 14px;
  color: var(--text);
  line-height: 1.5;
  margin-bottom: 16px;
}

.mentor-expertise {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.tag {
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 12px;
  color: var(--text);
}

.mentor-footer {
  display: flex;
  justify-content: stretch;
}

.mentor-footer .btn {
  width: 100%;
  justify-content: center;
}
</style>
