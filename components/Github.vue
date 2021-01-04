<template>
    <div class="entry github">
        <section v-for="project in projects" :key="project.name">
            <img v-if="project.image" :src="project.image" class="image">
            <img v-else src="~/static/github.png" class="image">
            <div class="desc">{{ project.desc }}</div>
        </section>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data: function () {
        return {
             projects: [
                 
             ]
        }
    },
    mounted() {
                axios.get("https://api.github.com/users/grubtub19/repos")
        .then(response => {
            console.log(response)
            response.data.forEach(project => {
                console.log(project.name)
                if(project.stargazers_count > 0) {
                    
                    var project_entry = {}
                    project_entry.name = project.name;
                    project_entry.desc = project.description;
                    
                    axios.get("https://api.github.com/repos/grubtub19/" + project.name + "/readme")
                    .then(readme => {
                        var img_regex = /!\[.*\]\((.*)\)/g
                        var description = atob(readme.data.content)
                        var result_array
                        // Loop through all image links in the readme
                        var regex_results_array
                        while(regex_results_array = img_regex.exec(description)) {

                            //Use the first image
                            project_entry.image = regex_results_array[1]
                        }
                        this.projects.push(project_entry)
                        console.log(project_entry.image)
                    })
                    .catch(error => {
                        console.log(error.response)
                    })
                }
            })
        })
        .catch(error => {
            console.log(error.response)
        })
    }
}
</script>
<style lang='scss'>

</style>