<template>
  <div class="student-details bg-white rounded">
    <div class="d-flex flex-column gap-3">
      <div class="d-flex align-items-center gap-3 ">
        <img
          class="rounded-circle"
          style="width: 65px; height: 65px;"
          src="../../assets/img/student-img.png"
          alt="Student Image"
        />
        <div class="d-flex flex-column">
          <div class="fullname fw-bold">{{ fullName }}</div>
          <div class="reg-copy">Reg. ID: {{ studentID }}
            <i class="material-icons toCopy" @click="copyDetails" title="Copy">{{ iconManager.copy }}</i>
          </div>
        </div>
      </div>
      <span class="status">Status: Active</span>
      <div>
        <div class="d-flex justify-content-between">
          <template v-for="(icon, iconName) in iconManager">
            <i
              v-if="iconName !== 'copy'"
              :key="iconName"
              class="material-icons rounded"
            >{{ icon }}</i>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { IconManager } from '../../utils/iconManager.js';
import studentProfile from '../../data/studentProfile.json';

export default {
  name: 'StudentDetails',
  data() {
    const { editNote, chat, today, email, phone, more, copy } = IconManager;
    return {
      iconManager: { editNote, chat, today, email, phone, more, copy },
      selectedIcon: '', 
      studentProfile: studentProfile,
    };
  },
  computed: {
    fullName() {
      const { aboutinfo } = this.studentProfile.studentProfile;
      return `${aboutinfo['First Name']} ${aboutinfo['Last Name']}`;
    },
    studentID() {
      return this.studentProfile.studentProfile.careerdetails.careers[0].studentID; 
    },
  },
methods: {
    selectIcon(iconName) {
      this.selectedIcon = iconName === this.selectedIcon ? '' : iconName;
    },
    copyDetails() {
      const fullName = this.fullName;
      const studentID = this.studentID;
      const textToCopy = `Nombre: ${fullName}, ID: ${studentID}`;
      navigator.clipboard.writeText(textToCopy)
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../../assets/scss/components/profile/_student-details.scss';
@import '../../assets/scss/components/profile/profile.scss';
</style>