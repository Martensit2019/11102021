<template>
  <div>
    <!-- withoutProgram-{{ withoutProgram }} -->
    <div v-if="course.type === 'module'">
      <EducationPlanElementAccordion :program="program" :course="course" :currentCourse="currentCourse" />
    </div>
    <div class="course mt_1" v-else-if="course.type === 'course'">
      <EducationPlanElementAccordion :program="program" :course="course" :currentCourse="currentCourse" />
      <!-- 000{{ course }} -->
      <!-- <div class="course__rating course_rating_excellent">5</div>
      <NuxtLink class="course__progress_info" to="/">
        <div class="course__name">{{ course.name }}</div>
        <div class="course__duration">11 дней</div>
        <div class="course__percent">{{ course.success_rate }}%</div>
      </NuxtLink>
      <progress-bar size="sm" themes="green" :progress="100" /> -->
    </div>
    <div v-else>
      <EducationPlanElementListItemBody
        :program="program"
        :course="course"
        :withoutProgram="withoutProgram"
         :currentCourse="currentCourse"
      />
    </div>
  </div>
</template>

<script>
import EducationPlanElementAccordion from "~/components/programs/layouts/EducationPlanElementAccordion";
import EducationPlanElementListItemBody from "~/components/programs/layouts/EducationPlanElementListItemBody";
import ProgressBar from "~/components/common/ProgressBar";
export default {
  name: "course-item",
  components: {
    EducationPlanElementAccordion: () =>
      import("./EducationPlanElementAccordion.vue"),
    EducationPlanElementListItemBody,
    ProgressBar
  },
  props: {
    program: {
      type: Object,
      default: null
    },
    course: {
      type: Object,
      default: null
    },
    withoutProgram: {
      type: Boolean,
      default: false
    },
    currentCourse: {
      type: String,
      default: null
    }
  }
};
</script>

<style></style>
