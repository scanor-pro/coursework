# Konekt: Student & Graduate University Connection Platform

Konekt is a fully responsive Vue 3 single-page application built as part of Web Programming Assignments (Assignment 1). It connects undergraduate students and prospective graduate candidates with top-tier universities, graduate student mentors, and an interactive community Q&A feed.

## Theme & Intended Audience
- **Theme**: Academic networking and university admission guidance.
- **Audience**: Undergraduate students exploring graduate programs, prospective PhD candidates, graduate student mentors from top institutions (Stanford, MIT, Oxford, etc.), and university recruiters.
- **Main Message**: Connecting ambitious students and graduate scholars to simplify university applications, mentorship, and academic planning.

## Key Features
1. **Interactive University Explorer**: Filter universities by degree level (Undergraduate, Graduate, PhD) and search by field or location with tuition and deadline details.
2. **Graduate Mentor Directory**: Direct 1-on-1 consultation requests with graduate student mentors and PhD candidates.
3. **Student & Graduate Community Q&A**: Interactive forum where students post questions and graduate mentors reply.
4. **Responsive Modern UI**: Built with Vue 3 Composition API (`ref`, `computed`) and modern Vanilla CSS featuring an academic navy/gold color palette.

## Project Structure
- `src/App.vue`: Main application container incorporating header, hero banner, modals, and footer.
- `src/components/UniversityExplorer.vue`: University program cards and filter logic.
- `src/components/MentorDirectory.vue`: Mentor profile cards and mentorship request workflow.
- `src/components/CommunityQA.vue`: Interactive Q&A discussion feed.
- `src/style.css`: Global design system and responsive grid styles.

## Installation & Running Locally

1. Install dependencies:
   ```bash
   npm install
   ```

2. Run the development server:
   ```bash
   npm run dev
   ```

3. Build for production:
   ```bash
   npm run build
   ```

## Prompt Records (Assignment 1 Compliance)
- **Initial Prompt**: "I would like a web application called 'Konekt' for connecting students and graduate students to top-tier universities. It should include university program search by degree level, graduate mentor directories, an interactive Q&A community feed, and clean academic styling with responsive mobile support."
- **Follow-up Prompt 1**: "Please add interactive modal dialogs when users click 'Inquire & Connect' on universities or 'Request Mentorship' on mentors, with success feedback messages."
- **Follow-up Prompt 2**: "Refine the Q&A community feed to allow students to post new questions and graduate mentors to reply directly inline."
