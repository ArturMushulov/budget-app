<template>
    <el-card class="form-card">
        <el-form :model="formData" :rules="rules" label-position="left" ref="formData">
            <el-form-item label="Type" prop="type">
                <el-select class="type-select" v-model="formData.type" placeholder="Choose type...">
                    <el-option label="Outcome" value="OUTCOME"></el-option>
                    <el-option label="Income" value="INCOME"></el-option>
                </el-select>
            </el-form-item>
            <el-form-item  label="Comments" prop="comment">
                <el-input v-model="formData.comment"/>
            </el-form-item>
            <el-form-item  label="Value" prop="value">
                <el-input v-model.number="formData.value" placeholder="Input number"/>
            </el-form-item>
            <el-button @click="onSubmit('formData')" type="primary"> 
                Submit
            </el-button>
        </el-form>
    </el-card>
</template>

<script>
export default {
    name: "AddForm",
    data: () => ({
        formData: {
            type: "",
            comment: "",
            value: null
        },
        rules: {
            type: [
                { required: true, message: "Please select type",  trigger: "blur" }
            ],
            comment: [
                { required: true, message: "Please  something write",  trigger: "change" }
            ],
            value: [
                { required: true, message: "Please  input value",  trigger: "change" },
                { type: "number", message: "Input number",  trigger: "submit" }
            ]
        }
    }),
    methods: {
        onSubmit(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    this.$emit("submitForm", { ...this.formData })
                    this.$refs[formName].resetFields();
                } else {
                    console.log('error submit!!');
                    return false;
                }
        });
        }
    }
}
</script>

<style scoped>
    .form-card {
        max-width: 500px;
        margin: auto;
    }
    .type-select {
        width: 100%;
    }
</style>