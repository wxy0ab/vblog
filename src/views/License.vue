<template>
    <div>
        <el-card shadow="never" style="min-height: 400px;margin-bottom: 20px;padding: 20px 0px 20px 0px;text-align: center">
            <div v-html="$markdown(text)" class="markdown-body" v-if="text"></div>
            <div style="min-height: 400px;margin-bottom: 20px;padding: 20px 0px 20px 0px;text-align: center" v-else>
            <font style="font-size: 30px;color:#dddddd ">
                <b>◔ ‸◔？</b>
            </font>
             </div>
        </el-card>
    </div>
</template>
<script>
    import ProjectApi from '@/api/project'
    export default {
        data() {
            return {
                loading: false,
                text: ""
            }
        },
        mounted() {
            this.loading = true
            ProjectApi.getBlogLicense().then((response) => {
                let result = response.data
                let base64 = require('js-base64').Base64
                this.text = base64.decode(result.content)
            }).then(() => this.loading = false).catch(() => this.loading = false)
        }
    }
</script>