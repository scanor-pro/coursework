<script setup>
import { ref } from 'vue'

const questions = ref([
  {
    id: 1,
    author: 'Liam (Undergrad CS Junior)',
    question: 'How important are undergraduate research publications for getting into top-5 PhD programs in Computer Science?',
    answers: [
      { author: 'Dr. Elena Rostova (Stanford PhD)', text: 'Having at least one workshop or conference paper significantly strengthens your application, but strong recommendation letters and rigorous coursework matter just as much!' }
    ],
    newAnswerText: ''
  },
  {
    id: 2,
    author: 'Sophia (Economics Senior)',
    question: 'What is the best way to approach professors for strong academic reference letters when classes were mostly large lecture halls?',
    answers: [
      { author: 'Aisha Al-Mansoor (Oxford DPhil)', text: 'Attend office hours early, share your term paper drafts or project ideas, and ask if they can speak to your specific intellectual curiosity.' }
    ],
    newAnswerText: ''
  }
])

const newQuestionTitle = ref('')
const newQuestionAuthor = ref('')

const addQuestion = () => {
  if (!newQuestionTitle.value.trim()) return
  questions.value.unshift({
    id: Date.now(),
    author: newQuestionAuthor.value.trim() || 'Anonymous Student',
    question: newQuestionTitle.value.trim(),
    answers: [],
    newAnswerText: ''
  })
  newQuestionTitle.value = ''
  newQuestionAuthor.value = ''
}

const addAnswer = (q) => {
  if (!q.newAnswerText.trim()) return
  q.answers.push({
    author: 'Konekt Mentor',
    text: q.newAnswerText.trim()
  })
  q.newAnswerText = ''
}
</script>

<template>
  <section id="community">
    <div class="container">
      <div class="section-header">
        <h2>Student & Graduate Q&A Community</h2>
        <p>Ask admission questions, discuss university choices, and get insights directly from graduate student mentors.</p>
      </div>

      <div class="qa-container">
        <!-- Ask Question Card -->
        <div class="card ask-card">
          <h3>Ask the Graduate Community</h3>
          <div class="form-group">
            <label>Your Name / Status</label>
            <input type="text" v-model="newQuestionAuthor" placeholder="e.g. Alex (Pre-Med Junior)" class="form-control" />
          </div>
          <div class="form-group">
            <label>Your Question</label>
            <textarea v-model="newQuestionTitle" placeholder="What would you like to ask graduate mentors or university alumni?" class="form-control" rows="3"></textarea>
          </div>
          <button class="btn btn-accent" @click="addQuestion">Post Question</button>
        </div>

        <!-- Questions Feed -->
        <div class="qa-feed">
          <div v-for="q in questions" :key="q.id" class="card qa-card">
            <div class="qa-header">
              <span class="qa-author">👤 {{ q.author }}</span>
            </div>
            <h4 class="qa-title">{{ q.question }}</h4>

            <div class="answers-list" v-if="q.answers.length > 0">
              <div v-for="(ans, idx) in q.answers" :key="idx" class="answer-item">
                <p class="answer-author">🎓 <strong>{{ ans.author }}:</strong></p>
                <p class="answer-text">{{ ans.text }}</p>
              </div>
            </div>

            <div class="add-answer-box">
              <input 
                type="text" 
                v-model="q.newAnswerText" 
                placeholder="Write a graduate mentor response..." 
                class="form-control"
                @keyup.enter="addAnswer(q)"
              />
              <button class="btn" @click="addAnswer(q)">Reply</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.qa-container {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 32px;
  align-items: start;
}

.ask-card {
  position: sticky;
  top: 96px;
}

.qa-feed {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.qa-card {
  margin-bottom: 0;
}

.qa-author {
  font-size: 13px;
  font-weight: 600;
  color: var(--primary);
  display: inline-block;
  margin-bottom: 8px;
}

.qa-title {
  font-size: 18px;
  color: var(--text-h);
  margin: 0 0 16px 0;
  line-height: 1.4;
}

.answers-list {
  background: var(--bg);
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
  border: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.answer-item {
  font-size: 14px;
}

.answer-author {
  margin: 0 0 4px 0;
  color: var(--text-h);
}

.answer-text {
  margin: 0;
  color: var(--text);
  line-height: 1.4;
}

.add-answer-box {
  display: flex;
  gap: 12px;
}

@media (max-width: 900px) {
  .qa-container {
    grid-template-columns: 1fr;
  }
  .ask-card {
    position: static;
  }
}
</style>
