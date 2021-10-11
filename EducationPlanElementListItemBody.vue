<template>
  <div>
    <!-- 000{{withoutProgram}}<br>
    currentCourse: {{currentCourse}} -->

    <div class="course mt_1" v-if="course.slug">
      <div class="course__rating course_rating_excellent">5</div>
      <NuxtLink
        class="course__progress_info"
        v-if="withoutProgram && course.type === 'lesson'"
        :to="{
          name: 'programs-program_id-lesson_id',
          params: {
            program_id: program.id,
            lesson_id: course.id
          }
        }"
      >
        <div class="course__name">{{ course.name }}</div>
        <div class="course__duration">11 дней</div>
        <div class="course__percent">{{ course.success_rate }}%</div>
      </NuxtLink>
      <NuxtLink
        class="course__progress_info"
        v-else-if="withoutProgram && course.type === 'kim'"
        to="/kim"
      >
        <div class="course__name">{{ course.name }}</div>
        <div class="course__duration">11 дней</div>
        <div class="course__percent">{{ course.success_rate }}%</div>
      </NuxtLink>
      <NuxtLink
        class="course__progress_info"
        v-else-if="!withoutProgram && course.type === 'lesson'"
        :to="{
          name: 'programs-program_id-course_id-lecture_id',
          params: {
            program_id: this.currentProgramSlug,
            course_id: this.currentCourse,
            lecture_id: course.slug
          }
        }"
      >
        <div class="course__name">{{ course.name }}</div>
        <div class="course__duration">11 дней</div>
        <div class="course__percent">{{ course.success_rate }}%</div>
      </NuxtLink>
      <NuxtLink
        class="course__progress_info"
        v-else-if="!withoutProgram && course.type === 'kim'"
        to="/kim/1"
      >
        <div class="course__name">{{ course.name }}</div>
        <div class="course__duration">11 дней</div>
        <div class="course__percent">{{ course.success_rate }}%</div>
      </NuxtLink>
      <progress-bar size="sm" themes="green" :progress="100" />
    </div>
  </div>
</template>

<script>
import ProgressBar from "~/components/common/ProgressBar";
import EducationPlanElementAccordion from "~/components/programs/layouts/EducationPlanElementAccordion";
import EducationPlanElement from "~/components/programs/layouts/EducationPlanElement";
export default {
  name: "course-item",
  components: {
    ProgressBar,
    EducationPlanElementAccordion,
    EducationPlanElement
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
  },
  data() {
    return {
      currentProgramSlug: null
    };
  },
  created() {
    this.currentProgramSlug = this.$route.params.program_id;
  }
};
</script>

<style></style>
