<script setup>
import { ref } from 'vue'
import UniversityExplorer from './components/UniversityExplorer.vue'
import MentorDirectory from './components/MentorDirectory.vue'
import CommunityQA from './components/CommunityQA.vue'

const activeModal = ref(null) // 'uni' or 'mentor'
const selectedTarget = ref(null)
const inquiryForm = ref({ name: '', email: '', message: '' })
const successMessage = ref('')

const openUniModal = (uni) => {
  selectedTarget.value = uni
  activeModal.value = 'uni'
  successMessage.value = ''
  inquiryForm.value = { name: '', email: '', message: `I am interested in applying to ${uni.name} for ${uni.field}. Please send admission guidelines.` }
}

const openMentorModal = (mentor) => {
  selectedTarget.value = mentor
  activeModal.value = 'mentor'
  successMessage.value = ''
  inquiryForm.value = { name: '', email: '', message: `Hi ${mentor.name}, I would love to connect for mentorship regarding ${mentor.expertise}.` }
}

const closeModal = () => {
  activeModal.value = null
  selectedTarget.value = null
}

const submitInquiry = () => {
  if (!inquiryForm.value.name || !inquiryForm.value.email) {
    alert('Please provide your name and email.')
    return
  }
  successMessage.value = `Success! Your inquiry has been sent to ${selectedTarget.value.name || selectedTarget.value.name}. We will connect you shortly.`
  setTimeout(() => {
    closeModal()
  }, 2500)
}

const scrollToSection = (id) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <div id="app">
    <!-- Navbar -->
    <header class="navbar">
      <div class="container nav-content">
        <a href="#" class="logo">
          <div class="logo-icon">K</div>
          Konekt
        </a>
        <nav class="nav-links">
          <a @click="scrollToSection('universities')">Universities</a>
          <a @click="scrollToSection('mentors')">Graduate Mentors</a>
          <a @click="scrollToSection('community')">Community Q&A</a>
        </nav>
        <button class="btn btn-accent" @click="scrollToSection('universities')">Get Started</button>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero-section">
      <div class="container hero-content">
        <div class="badge">🎓 Student & Graduate University Connection Platform</div>
        <h1 class="hero-title">Bridge Your Academic Future to Top Universities</h1>
        <p class="hero-subtitle">
          Connect undergraduate students and prospective graduate candidates directly with graduate student mentors, PhD advisors, and world-class university programs.
        </p>
        <div class="hero-actions">
          <button class="btn btn-accent" @click="scrollToSection('universities')">Explore Programs</button>
          <button class="btn btn-outline" style="color: white; border-color: rgba(255,255,255,0.4);" @click="scrollToSection('mentors')">Find a Mentor</button>
        </div>

        <div class="hero-stats">
          <div class="stat-item">
            <h3>150+</h3>
            <p>Partner Universities</p>
          </div>
          <div class="stat-item">
            <h3>2,500+</h3>
            <p>Graduate Mentors</p>
          </div>
          <div class="stat-item">
            <h3>98%</h3>
            <p>Admission Guidance Success</p>
          </div>
        </div>
      </div>
    </section>

    <!-- University Explorer Component -->
    <UniversityExplorer @selectUni="openUniModal" />

    <!-- Mentor Directory Component -->
    <MentorDirectory @requestMentorship="openMentorModal" />

    <!-- Community Q&A Component -->
    <CommunityQA />

    <!-- Footer -->
    <footer>
      <div class="container">
        <div class="footer-content">
          <div class="footer-col">
            <h4>Konekt Platform</h4>
            <p>Empowering students and graduate scholars worldwide to connect with top-tier universities and mentors.</p>
          </div>
          <div class="footer-col">
            <h4>Quick Links</h4>
            <a @click="scrollToSection('universities')">Top Universities</a>
            <a @click="scrollToSection('mentors')">Graduate Mentors</a>
            <a @click="scrollToSection('community')">Student Q&A</a>
          </div>
          <div class="footer-col">
            <h4>Assignment 1 Compliance</h4>
            <p>Built with Vue 3 & Vite following Web Programming Assignment guidelines. Single static page application with rich interactivity.</p>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2026 Konekt. All rights reserved. Designed for Student & Graduate University Networking.</p>
        </div>
      </div>
    </footer>

    <!-- Inquiry / Mentorship Modal -->
    <div v-if="activeModal" class="modal-overlay" @click.self="closeModal">
      <div class="modal">
        <h3>{{ activeModal === 'uni' ? 'Inquire about ' + selectedTarget.name : 'Request Mentorship with ' + selectedTarget.name }}</h3>
        
        <div v-if="successMessage" class="success-banner">
          {{ successMessage }}
        </div>

        <div v-else>
          <div class="form-group">
            <label>Your Full Name</label>
            <input type="text" v-model="inquiryForm.name" placeholder="Enter your name" class="form-control" />
          </div>
          <div class="form-group">
            <label>Your Email Address</label>
            <input type="email5" v-model="inquiryForm.email" placeholder="student@university.edu" class="form-control" />
          </div>
          <div class="form-group">
            <label>Message / Statement</label>
            <textarea v-model="inquiryForm.message" rows="4" class="form-control"></textarea>
          </div>
          <div class="modal-actions">
            <button class="btn btn-outline" @click="closeModal">Cancel</button>
            <button class="btn" @click="submitInquiry">Send Request</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.success-banner {
  background: #d1fae5;
  color: #065f46;
  padding: 16px;
  border-radius: 8px;
  text-align: center;
  font-weight: 600;
  margin-bottom: 20px;
}
</style>
