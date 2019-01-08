<template>
    <div style="width: 340px">
        <div class="filter-label">
            <b>Custom Skills Filter</b>
        </div>
        <label v-for="(skill, index) in RefData.IT_SKILLS"
               class="filter">
            <span>
                <div style="text-align: center">{{RefData.IT_SKILLS_NAMES[index]}}</div>
                <div>
                    <input type="checkbox" @click="onSkillChanged(skill, $event)"/>
                    <img :src="`images/skills/${skill}.png`" width="30"/>
                </div>
            </span>
        </label>
    </div>
</template>

<script>
    import RefData from '../utils/RefData';

    export default {
        name: 'SkillFilter',
        data() {
            return {
                android: false,
                css: false,
                html5: false,
                mac: false,
                windows: false,
                skillsTemplates: [],
                RefData
            }
        },
        methods: {
            getModel() {
                return {
                    android: this.android,
                    css: this.css,
                    html5: this.html5,
                    mac: this.mac,
                    windows: this.windows
                }
            },
            setModel(model) {
                this.android = model ? model.android : null;
                this.css = model ? model.css : null;
                this.html5 = model ? model.html5 : null;
                this.mac = model ? model.mac : null;
                this.windows = model ? model.windows : null;
            },
            // called by agGrid
            doesFilterPass(params) {
                const rowSkills = params.data.skills;
                let passed = true;

                RefData.IT_SKILLS.forEach((skill) => {
                    if (this[skill]) {
                        if (!rowSkills[skill]) {
                            passed = false;
                        }
                    }
                });

                return passed;
            },
            getModel() {
                return ''
            },
            // called by agGrid
            isFilterActive() {
                return this.android || this.css || this.html5 || this.mac || this.windows;
            },

            onSkillChanged(skill, event) {
                this[skill] = event.target.checked;
                this.params.filterChangedCallback();
            }
        },
    }
</script>

<style scoped>
    .filter {
        border: 1px solid lightgrey;
        margin: 4px;
        padding: 4px;
        display: inline-block !important;
    }

    .filter-label {
        text-align: center;
        background: lightgray;
        width: 100%;
        display: block;
        border-bottom: 1px solid grey;
    }
</style>
