<template>

    <ResumeForm :form="form" @update:form="form = $event" />
    <ResumePreview :form="form" />
<div class="relative">
  <button
    @click="downloadPDF"
    class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg shadow-md transition duration-300 ease-in-out transform hover:scale-105 absolute -left-[506px] top-[102%]"
  >
    Download PDF
  </button>
</div>



</template>
<script>
import ResumeForm from "@/components/ResumeForm.vue"; // If using aliases


import ResumePreview from '@/components/ResumePreview.vue';
import html2pdf from 'html2pdf.js';

export default {
  components: { ResumeForm, ResumePreview },
  data() {
    return {
      form: {
        name: '',
        jobTitle: '',
        location: '',
        phone: '',
        email: '',
        profile: '',
        links: [],
        primarySkills: [],
        education: [],
        technicalSkills: [],
        projects: [
          {
            name: '',
            url: '',
            description: '',
            techStack: []
          }
        ],
        courses: []
      }
    };
  },
  mounted() {
    document.body.style.zoom = "80%";
  },
  methods: {
    downloadPDF() {
      const element = document.getElementById('resume-content');
      html2pdf(element, {
        margin: 10,
        filename: 'resume.pdf',
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2 },
        jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
      });
    }
  }
};
</script>
