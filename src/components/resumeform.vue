<template>
<div class="max-w-3xl mx-auto bg-white shadow-lg rounded-xl p-6 space-y-6 border-t-4 border-blue-600 w-[771px]">
  <!-- Header -->
  <header class="text-center p-3">
    <div class="flex justify-between items-center mb-4">
      <h2 class="font-bold text-xl text-gray-800">Personal Details</h2>
      <button @click="toggleSection('header')" class="text-gray-600 hover:text-blue-600 transition">
        <i :class="headerVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
      </button>
    </div>

    <transition name="fade">
      <div v-show="headerVisible">
        <!-- Full Name -->
        <div class="mb-4">
          <label class="block font-semibold text-gray-700 mb-1">Full Name</label>
          <input type="text" v-model="form.name" placeholder="Enter your full name" class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
        </div>

        <!-- Job Title -->
        <div class="mb-4">
          <label class="block font-semibold text-gray-700 mb-1">Job Title</label>
          <input type="text" v-model="form.jobTitle" placeholder="Enter your job title" class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
        </div>

        <!-- Contact Details -->
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4 text-sm text-gray-600">
          <div>
            <label class="block font-medium mb-1">Location</label>
            <input type="text" v-model="form.location" placeholder="Enter location" class="w-full px-3 py-2 border rounded-lg">
          </div>

          <div>
            <label class="block font-medium mb-1">Phone</label>
            <input type="tel" v-model="form.phone" placeholder="Enter phone number" class="w-full px-3 py-2 border rounded-lg">
          </div>

          <div>
            <label class="block font-medium mb-1">Email</label>
            <input type="email" v-model="form.email" placeholder="Enter email" class="w-full px-3 py-2 border rounded-lg">
          </div>
        </div>

        <!-- Links Section -->
        <div class="mt-4">
          <label class="block font-medium text-gray-700 mb-2">Links</label>
          <div v-for="(link, index) in form.links" :key="index" class="flex items-center gap-2 mb-2">
            <input type="text" v-model="link.name" placeholder="Link Name" class="flex-1 px-3 py-2 border rounded-lg">
            <input type="url" v-model="link.url" placeholder="Link URL" class="flex-1 px-3 py-2 border rounded-lg">
            <button @click="removeLink(index)" class="text-red-500 hover:text-red-700 text-xl">&times;</button>
          </div>
          <button @click="addLink" class="text-blue-500 hover:text-blue-700 font-medium">+ Add Another Link</button>
        </div>
      </div>
    </transition>
  </header>


    <!-- Profile -->
<section class="container mt-4">
<!-- Profile -->
<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-blue-600">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Profile Description</h2>
    <button @click="toggleSection('profile')" class="text-gray-600 hover:text-blue-600 transition">
      <i :class="profileVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="profileVisible">
      <textarea v-model="form.profile" rows="5" class="w-full px-4 py-3 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700"></textarea>
    </div>
  </transition>
</section>

<!-- Primary Skills -->
<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-green-600">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Primary Skills</h2>
    <button @click="toggleSection('primarySkills')" class="text-gray-600 hover:text-green-600 transition">
      <i :class="primarySkillsVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="primarySkillsVisible">
      <div class="space-y-3">
        <div v-for="(skill, index) in form.primarySkills" :key="'primary-' + index" class="flex items-center gap-3">
          <input type="text" v-model="form.primarySkills[index]" placeholder="Primary Skill" class="flex-1 px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-green-500 focus:outline-none">
          <button @click="removePrimarySkill(index)" class="text-red-500 hover:text-red-700 text-xl">&times;</button>
        </div>
      </div>
      <button @click="addPrimarySkill" class="mt-3 text-green-600 hover:text-green-700 font-medium">+ Add Primary Skill</button>
    </div>
  </transition>
</section>






<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-purple-600">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Education</h2>
    <button @click="toggleSection('education')" class="text-gray-600 hover:text-purple-600 transition">
      <i :class="educationVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="educationVisible">
      <div v-for="(education, index) in form.education" :key="index" class="bg-gray-50 border border-gray-200 rounded-lg p-4 shadow-sm mb-4">
        <div class="mb-3">
          <label class="block text-gray-700 font-medium mb-1">Degree</label>
          <input type="text" v-model="education.degree" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-purple-500 focus:outline-none text-gray-700" placeholder="e.g., Bachelor’s Degree">
        </div>

        <div class="mb-3">
          <label class="block text-gray-700 font-medium mb-1">Institution</label>
          <input type="text" v-model="education.institution" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-purple-500 focus:outline-none text-gray-700" placeholder="e.g., University Name">
        </div>

        <div class="mb-3">
          <label class="block text-gray-700 font-medium mb-1">Duration</label>
          <input type="text" v-model="education.duration" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-purple-500 focus:outline-none text-gray-700" placeholder="e.g., 2020 - 2022">
        </div>

        <button @click="removeEducation(index)" class="text-red-600 hover:text-red-700 font-medium flex items-center">
          <i class="fas fa-trash-alt mr-2"></i> Remove
        </button>
      </div>

      <button @click="addEducation" class="mt-3 text-purple-600 hover:text-purple-700 font-medium flex items-center">
        <i class="fas fa-plus-circle mr-2"></i> Add Education
      </button>
    </div>
  </transition>
</section>


<!-- Technical Skills Section -->
<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-blue-600">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Technical Skills</h2>
    <button @click="toggleSection('technicalSkills')" class="text-gray-600 hover:text-blue-600 transition">
      <i :class="technicalSkillsVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="technicalSkillsVisible">
      <div v-for="(skill, index) in form.technicalSkills" :key="'technical-' + index" class="flex items-center gap-3 bg-gray-50 border border-gray-200 rounded-lg p-3 shadow-sm mb-3">
        <input type="text" v-model="form.technicalSkills[index]" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700" placeholder="e.g., JavaScript">

        <button @click="removeTechnicalSkill(index)" class="text-red-600 hover:text-red-700 font-medium flex items-center px-3 py-2 rounded transition">
          <i class="fas fa-trash-alt mr-2"></i> Remove
        </button>
      </div>

      <button @click="addTechnicalSkill" class="mt-3 text-blue-600 hover:text-blue-700 font-medium flex items-center">
        <i class="fas fa-plus-circle mr-2"></i> Add Technical Skill
      </button>
    </div>
  </transition>
</section>


</section>

<!-- Projects Section -->
<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-blue-600 w-[700px]">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Projects</h2>
    <button @click="toggleSection('projects')" class="text-gray-600 hover:text-blue-600 transition">
      <i :class="projectsVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="projectsVisible">
      <div v-for="(project, index) in form.projects" :key="index" class="bg-gray-50 border border-gray-200 rounded-lg p-4 shadow-sm mb-4">

        <div class="mb-3">
          <label class="block text-gray-700 font-medium">Project Name</label>
          <input type="text" v-model="project.name" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700" placeholder="e.g., Music-Vibe - Streaming Platform">
        </div>

        <div class="mb-3">
          <label class="block text-gray-700 font-medium">Project URL</label>
          <input type="url" v-model="project.url" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700" placeholder="e.g., https://example.com">
        </div>

        <div class="mb-3">
          <label class="block text-gray-700 font-medium">Description</label>
          <textarea v-model="project.description" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700" rows="3" placeholder="Briefly describe the project..."></textarea>
        </div>

        <div class="mb-3">
          <label class="block text-gray-700 font-medium">Tech Stack</label>
          <input
            type="text"
            v-model="project.techStackInput"
            class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700"
            placeholder="e.g., Vue.js, Bootstrap, Firebase"
            @keyup.enter="addTechStack(index)"
          >

          <!-- Tech Stack Badges -->
          <div class="mt-3 flex flex-wrap gap-2">
            <span v-for="(tech, techIndex) in project.techStack" :key="'tech-' + techIndex" class="bg-blue-600 text-white px-3 py-1 rounded-full flex items-center">
              {{ tech }}
              <button @click="removeTechStack(index, techIndex)" class="ml-2 text-white hover:text-gray-300">&times;</button>
            </span>
          </div>
        </div>

        <button @click="removeProject(index)" class="mt-3 bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg shadow-md transition">
          <i class="fas fa-trash-alt mr-2"></i> Remove Project
        </button>

      </div>

      <button @click="addProject" class="mt-4 text-blue-600 hover:text-blue-700 font-medium flex items-center">
        <i class="fas fa-plus-circle mr-2"></i> Add Project
      </button>
    </div>
  </transition>
</section>


<!-- Courses & Certifications Section -->
<section class="container mt-6 bg-white shadow-lg rounded-lg p-6 border-l-4 border-blue-600 w-[700px]">
  <div class="flex justify-between items-center mb-4">
    <h2 class="text-xl font-semibold text-gray-800">Courses & Certifications</h2>
    <button @click="toggleSection('courses')" class="text-gray-600 hover:text-blue-600 transition">
      <i :class="coursesVisible ? 'fas fa-chevron-up' : 'fas fa-chevron-down'"></i>
    </button>
  </div>

  <transition name="fade">
    <div v-show="coursesVisible">
      <div v-for="(course, index) in form.courses" :key="'course-' + index" class="bg-gray-50 border border-gray-200 rounded-lg p-4 shadow-sm mb-4 flex items-center">
        <span class="text-blue-500 text-lg">•</span>
        <div class="flex-grow ml-3">
          <input type="text" v-model="course.title" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700" placeholder="Course Name (e.g., Complete Node.js Developer Course)">
          <input type="text" v-model="course.platform" class="w-full px-4 py-2 border rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none text-gray-700 mt-2" placeholder="Platform/Provider (e.g., Udemy)">
        </div>
        <button @click="removeCourse(index)" class="ml-3 bg-red-500 hover:bg-red-600 text-white px-3 py-2 rounded-lg shadow-md transition">
          <i class="fas fa-trash-alt"></i>
        </button>
      </div>

      <button @click="addCourse" class="mt-4 text-blue-600 hover:text-blue-700 font-medium flex items-center">
        <i class="fas fa-plus-circle mr-2"></i> Add Course
      </button>
    </div>
  </transition>
</section>


</div>
</template>
<script>
export default {
  props: ['form'],
  emits: ['update:form'],
    data() {
    return {
      headerVisible: false,
      profileVisible: false,
      skillsVisible: false,
        primarySkillsVisible: false,
        educationVisible: false,
        technicalSkillsVisible: false,
        projectsVisible: false,
         coursesVisible: false,
    };
  },

  methods: {

       // Toggle sections
    toggleSection(section) {
      this[`${section}Visible`] = !this[`${section}Visible`];
    },
    // Links
    addLink() {
      this.form.links.push({ name: '', url: '' });
    },
    removeLink(index) {
      this.form.links.splice(index, 1);
    },

    // Primary Skills
    addPrimarySkill() {
      this.form.primarySkills.push('');
    },
    removePrimarySkill(index) {
      this.form.primarySkills.splice(index, 1);
    },

    // Technical Skills
    addTechnicalSkill() {
      this.form.technicalSkills.push('');
    },
    removeTechnicalSkill(index) {
      this.form.technicalSkills.splice(index, 1);
    },

    // Education
    addEducation() {
      this.form.education.push({ degree: '', institution: '', duration: '' });
    },
    removeEducation(index) {
      this.form.education.splice(index, 1);
    },

    // Projects
    addProject() {
      this.form.projects.push({
        name: '',
        url: '',
        description: '',
        techStack: [],
      });
    },
    removeProject(index) {
      this.form.projects.splice(index, 1);
    },

    // Add Tech Stack to project
    addTechStack(project) {
      if (project.techStackInput) {
        // Split the input by commas and trim whitespace
        const techStackItems = project.techStackInput.split(',').map(item => item.trim());

        // Add each tech stack item to the project
        project.techStack.push(...techStackItems);

        // Clear the input field after adding
        project.techStackInput = '';
      }
    },
    addCourse() {
      this.form.courses.push({ title: '', platform: '' });
    },

    // Remove a course from the list
    removeCourse(index) {
      this.form.courses.splice(index, 1);
    },
  }
};
</script>
<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease-in-out;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
