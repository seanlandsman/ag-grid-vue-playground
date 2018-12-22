<template>
    <span >
        <img v-for="skill in skills" :src='`https://www.ag-grid.com/images/skills/${skill}.png`' width=16 :title='skill'/>
    </span>
</template>

<script>
    import RefData from "../utils/RefData";

    export default {
        name: 'SkillsCellRenderer',
        data() {
            return {
                skills: []
            }
        },
        beforeMount() {
            RefData.IT_SKILLS.forEach((skill) => {
                if (this.params.data && this.params.data.skills && this.params.data.skills[skill]) {
                    this.skills.push(skill);
                }
            });
        }
    }
</script>
