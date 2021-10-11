<template>
  <div>
    <div
      v-b-toggle="'title-' + course.id"
      class="education-plan__header"
      @click="isOpen = !isOpen"
    >
      <div class="collapse__icon" :class="{ collapse_icon_open: isOpen }">
        <svg width="10" height="6" viewBox="0 0 10 6">
          <path
            d="M8.76117 0L5 3.61719L1.23883 0L0 1.19141L5 6L10 1.19141L8.76117 0Z"
            fill="#191919"
          />
        </svg>
      </div>
      <NuxtLink
        v-if="course.type !== 'semester' && course.type !== 'module'"
        class="education-plan__title"
        :to="{
          name: 'programs-program_id-course_id',
          params: {
            program_id: this.currentProgramSlug,
            course_id: course.slug
          }
        }"
      >
        {{ course.name }}
      </NuxtLink>
      <div v-else class="education-plan__title">{{ course.name }}</div>
      <div class="education-plan__arrow">
        <div class="education-plan__progress mr_4">
          {{ course.success_rate }}%
          <progress-bar
            size="md"
            themes="blue"
            :progress="course.success_rate"
          />
        </div>
      </div>
    </div>
    <b-collapse :id="'title-' + course.id" class="education-plan__body">
      <!-- {{ course }} -->
      <div v-if="course.type === 'course'">
        <template v-for="course_item in course.education_plan">
          <EducationPlanElementListItem :course="course_item" :currentCourse="course.slug" />
        </template>
      </div>
      <div v-else-if="course.type === 'semester' || course.type === 'module'">
        <template v-for="course_item in course.items">
          <EducationPlanElementListItem :course="course_item" :currentCourse="course.slug" />
        </template>
      </div>
    </b-collapse>
  </div>
</template>
<script>
import ProgressBar from "~/components/common/ProgressBar";
import EducationPlanElementListItem from "~/components/programs/layouts/EducationPlanElementListItem";
export default {
  name: "education-plan-element-accordion",
  components: { ProgressBar, EducationPlanElementListItem },
  props: {
    program: {
      type: Object,
      default: null
    },
    course: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      isOpen: false,
      currentProgramSlug: null
    }
  },
  created() {
    this.currentProgramSlug = this.$route.params.program_id;
  }
};
</script>
