<template>
<div class="max-w-3xl mx-auto bg-white shadow-md rounded-lg p-6 space-y-6 border-t-4 border-blue-600 w-[771px]" id="resume-content">


    <!-- Header -->
<header class="text-center space-y-2">
  <h1 class="text-3xl font-bold">{{ form.name || 'Your Name' }}</h1>
  <p class="text-sm font-semibold text-blue-600">{{ form.jobTitle || 'Your Job Title' }}</p>

  <div class="flex flex-wrap justify-center gap-4 text-sm text-gray-600">
    <div><i class="fas fa-map-marker-alt text-blue-500"></i><span class="ml-1">{{ form.location || 'City-Pincode, State, Country' }}</span></div>
    <div><i class="fas fa-phone text-blue-500"></i>
      <a :href="'tel:' + (form.phone || '')" class="hover:text-blue-600 ml-1">{{ form.phone || '+91-86388......' }}</a>
    </div>
    <div><i class="fas fa-envelope text-blue-500"></i>
      <a :href="'mailto:' + (form.email || '')" class="hover:text-blue-600 ml-1">{{ form.email || 'example@gmail.com' }}</a>
    </div>
    <div><i class="fas fa-globe text-blue-500"></i>
      <a :href="form.portfolio || ''" target="_blank" class="hover:text-blue-600 ml-1">
        {{ form.portfolioLabel || 'Portfolio' }}
      </a>
    </div>
    <div><i class="fab fa-github text-blue-500"></i>
      <a :href="form.github || ''" target="_blank" class="hover:text-blue-600 ml-1">
        {{ form.githubLabel || 'GitHub' }}
      </a>
    </div>
  </div>
</header>



<!-- Profile (Key Skills) -->
<section >
       <h2 class="text-xl font-bold text-gray-800 border-b pb-1">Profile</h2>
    <p class="text-sm mt-2 leading-relaxed">
        {{ form.profile || 'Motivated Full Stack Developer with practical experience building modern websites. Passionate about writing clean code and learning new technologies. Seeking an opportunity to contribute to a collaborative team and create impactful projects.' }}
    </p>

    <!-- Primary Skills Preview -->
    <div v-if="form.primarySkills && form.primarySkills.length" class="mt-3">
        <h3 class="text-sm font-semibold text-gray-700">Primary Skills:</h3>
        <div class="flex flex-wrap gap-2 mt-2">
            <span v-for="(skill, index) in form.primarySkills" :key="'primary-' + index"
                class="px-3 py-1 text-xs font-medium text-white bg-blue-400 rounded-full shadow-sm">
                {{ skill }}
            </span>
        </div>
    </div>
</section>


        <!-- Education -->
<section>
    <h2 class="text-xl font-bold text-gray-800 border-b pb-1">Education</h2>
    <ul class="text-sm mt-3 grid grid-cols-1 sm:grid-cols-2 gap-4">
        <!-- Loop through the education array -->
        <li v-for="(edu, index) in form.education" :key="index" class="flex items-start gap-2">
            <div class="w-2 h-2 mt-1 bg-blue-500 rounded-full"></div>
            <div>
                <!-- Display degree, institution, and duration dynamically with fallback values -->
                <strong class="block text-gray-800">{{ edu.degree || 'Degree Name' }}, {{ edu.institution || 'Institution' }}</strong>
                <span class="text-gray-600">{{ edu.duration || 'Duration' }}</span>
            </div>
        </li>
        <!-- If no education data, show a message indicating no data -->
        <li v-if="form.education.length === 0" class="text-gray-600">No education data available.</li>
    </ul>
</section>




<!-- Technical Skills -->
<section>
    <h2 class="text-xl font-bold text-gray-800 border-b pb-1">Technical Skills</h2>
    <ul class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-sm mt-3">
        <li v-for="(skill, index) in form.technicalSkills" :key="'technical-' + index" class="flex items-start gap-2">
            <span class="text-blue-500 font-bold">➤</span>
            <div class="text-gray-800">{{ skill }}</div>
        </li>
    </ul>
</section>

<section>
    <h2 class="text-xl font-bold text-gray-800 border-b pb-1">Projects</h2>
    <div class="text-sm space-y-3 mt-2">
        <div v-for="(project, index) in form.projects" :key="'project-' + index">
            <strong>{{ project.name }}</strong>
            <a :href="project.url" target="_blank" class="text-blue-600 ml-1">
                <i class="fas fa-link"></i>
            </a>
            <p>{{ project.description }}</p>
            <p class="text-xs text-gray-500">
                <strong>Tech-Stack:</strong>
                <!-- If techStack is an array, join the items with commas -->
                {{ project.techStack && project.techStack.length > 0 ? project.techStack.join(', ') : 'No tech stack provided' }}
            </p>
        </div>
    </div>
</section>



  <section>
    <h2 class="text-xl font-bold text-gray-800 border-b pb-1">Courses & Certifications</h2>
    <ul class="grid grid-cols-2 gap-x-8 gap-y-2 text-sm mt-2">
      <!-- Loop through the courses array and display each course dynamically -->
      <li v-for="(course, index) in form.courses" :key="index" class="flex items-start gap-1">
        <span class="text-gray-600">•</span>
        <span><strong>{{ course.title }}</strong> — {{ course.platform }}</span>
      </li>
    </ul>
  </section>



</div>
</template>

<script>
export default {
  props: ['form']
};
</script>

<style scoped>
.fixed-name {
  font-size: 24px;
  font-weight: bold;
}

.fixed-title {
  font-size: 14px;
  font-weight: 600;
  color: #2563EB;
}

.fixed-contacts {
  font-size: 12px;
  color: #4B5563;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
}

.icon {
  color: #3B82F6;
}
</style>
