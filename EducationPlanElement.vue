<template>
  <div class="education-plan__element">
    <div>
      <div
        v-if="
          education_plan_element.type === 'course' ||
            (education_plan_element.type === 'semester' &&
              education_plan_element.items)
        "
      >
        <EducationPlanElementAccordion
          :program="program"
          :course="education_plan_element"
        />
      </div>
      <div v-else>
        <!-- education_plan_element-{{ education_plan_element }} -->
        <EducationPlanElementListItem
          :program="program"
          :course="education_plan_element"
          :withoutProgram="true"
        />
      </div>
    </div>
  </div>
</template>

<script>
import EducationPlanElementAccordion from "~/components/programs/layouts/EducationPlanElementAccordion";
import EducationPlanElementListItem from "~/components/programs/layouts/EducationPlanElementListItem";
export default {
  name: "education-plan-element",
  components: {
    EducationPlanElementAccordion,
    EducationPlanElementListItem
  },
  props: {
    program: {
      type: Object,
      default: null
    },
    education_plan_element: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      isOpen: false
    };
  }
};
</script>

<style></style>
