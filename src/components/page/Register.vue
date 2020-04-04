<template>
    <div class="login-wrap">
        <div class="ms-login">
            <div class="ms-title">超级成绩单 - 注册页面</div>
            <el-form :model="ruleForm" label-width="0px" class="ms-content" :rules="rule" v-enterToNext="true">
                <el-form-item label="用户名" prop="username" labelWidth="80px">
                    <el-input v-model="ruleForm.username" placeholder="username">
                        <!--<el-button slot="prepend" icon="el-icon-lx-people"></el-button>-->
                    </el-input>
                </el-form-item>
                <el-form-item prop="password" label="密码" labelWidth="80px">
                    <el-input type="password" placeholder="password" v-model="ruleForm.password"
                              @keyup.enter.native="login">
                        <!--<el-button slot="prepend" icon="el-icon-lx-lock"></el-button>-->
                    </el-input>
                </el-form-item>
                <el-form-item prop="radio" style="text-align: center;">
                    <el-radio-group v-model="radioT">
                        <el-radio :label="3">学生</el-radio>
                        <el-radio :label="6">教师</el-radio>
                        <el-radio :label="9">学校管理员</el-radio>
                    </el-radio-group>
                </el-form-item>


                <!--学生-->
                <el-form id="student" :model="ruleForm_Stu" :rules="rule_stu" ref="ruleForm"  class="demo-ruleForm" style="display: none;">
                    <el-form-item label="学校" prop="school" labelWidth="80px">
                        <el-select type="password" v-model="stu_select_schoolS" placeholder="请选择学校">
                            <el-option
                                    v-for="item in schoolList"
                                    :key="item.school_ID"
                                    :label="item.school_NAME"
                                    :value="item.school_ID">
                            </el-option>
                        </el-select>
                    </el-form-item>

                    <el-form-item label="班级" prop="class" labelWidth="80px">
                        <el-select type="password" v-model="ruleForm_Stu.class" placeholder="请选择班级">
                            <el-option
                                    v-for="item in classList"
                                    :key="item.class_ID"
                                    :label="item.class_NAME"
                                    :value="item.class_ID">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="姓名" prop="name" labelWidth="80px">
                        <el-input v-model="ruleForm_Stu.name">
                        </el-input>
                    </el-form-item>
                    <el-form-item label="学号" prop="num" labelWidth="80px">
                        <el-input v-model="ruleForm_Stu.num">
                        </el-input>
                    </el-form-item>
                    <el-form-item style="text-align: center;">
                        <el-button type="primary" @click="studentR">学生注册</el-button>
                        <!--<el-button @click="resetForm('ruleForm_Stu')">重置</el-button>-->
                    </el-form-item>
                </el-form>


                <!--教师-->
                <el-form id="teacher" :model="ruleForm_Tea" :rules="rule_tea" ref="ruleForm" class="demo-ruleForm" style="display: none;">
                    <el-form-item label="学校" prop="school" labelWidth="80px">
                        <el-select v-model="stu_select_schoolT" placeholder="请选择学校">
                            <el-option
                                    v-for="item in schoolList"
                                    :key="item.school_ID"
                                    :label="item.school_NAME"
                                    :value="item.school_ID">
                            </el-option>
                        </el-select>
                    </el-form-item>

                    <el-form-item label="部门" prop="department" labelWidth="80px">
                        <el-select v-model="ruleForm_Tea.department" placeholder="请选择部门">
                            <el-option
                                    v-for="item in departmentList"
                                    :key="item.department_ID"
                                    :label="item.department_NAME"
                                    :value="item.department_ID">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="姓名" prop="name" labelWidth="80px">
                        <el-input v-model="ruleForm_Tea.name">
                        </el-input>
                    </el-form-item>
                    <el-form-item label="工号" prop="num" labelWidth="80px">
                        <el-input v-model="ruleForm_Tea.num">
                        </el-input>
                    </el-form-item>
                    <el-form-item style="text-align: center;">
                        <el-button type="primary" @click="teacherR">教师注册</el-button>
                    </el-form-item>
                </el-form>


                <!--学校-->
                <el-form id="school" :model="ruleForm_Sch" :rules="rule_sch" ref="ruleForm" class="demo-ruleForm" style="display: none;">
                    <el-form-item label="国家" prop="country" labelWidth="80px">
                        <el-select v-model="ruleForm_Sch.country" placeholder="请选择国家">
                            <el-option
                                    v-for="item in countryList"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="省份" prop="province" labelWidth="80px">
                        <el-select v-model="ruleForm_Sch.province" placeholder="请选择省份">
                            <el-option
                                    v-for="item in provinceList"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="城市" prop="city" labelWidth="80px">
                        <el-select v-model="ruleForm_Sch.city" placeholder="请选择城市">
                            <el-option
                                    v-for="item in cityList"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="学校" prop="name" labelWidth="80px">
                        <el-input v-model="ruleForm_Sch.name">
                        </el-input>
                    </el-form-item>
                    <el-form-item style="text-align: center;">
                        <el-button type="primary" @click="schoolR">学校注册</el-button>
                    </el-form-item>
                </el-form>

            </el-form>
        </div>
    </div>
</template>

<script>
    import md5 from 'js-md5';
    import ElFormItem from "../../../node_modules/element-ui/packages/form/src/form-item";


    export default {
        components: {ElFormItem}, name: 'login',
        data() {
            return {
                radioT: 0,
                visibleStu: true,
                visibleTea: false,
                visibleSch: false,
                schoolList:{},
                departmentList:{},
                classList:{},
                stu_select_schoolS: '',
                stu_select_schoolT: '',
                ruleForm: {
                    username: '',
                    password: '',
                },
                ruleForm_Stu: {
                    class:'',
                    name:'',
                    num:''
                },
                ruleForm_Tea: {
                    department:'',
                    name:'',
                    num:'',
                },
                ruleForm_Sch: {
                    country:'',
                    province:'',
                    city:'',
                    name:''
                },
                rule: {
                    username: [
                        {required: true, message: '请输入用户名', trigger: 'blur'},
                        {min: 3, max: 10, message: '请输入3到10个字符', trigger: 'blur'}
                    ],
                    password: [
                        {required: true, message: '请输入密码', trigger: 'blur'},
                        {min: 5, max: 12, message: '请输入5到12个字符', trigger: 'blur'}
                    ]
                },
                rule_stu:{
                    school: [
                        {required: true, message: '请选择学校', trigger: 'blur'}
                    ],
                    class: [
                        {required: true, message: '请选择班级', trigger: 'blur'}
                    ],
                    name: [
                        {required: true, message: '请输入姓名', trigger: 'blur'}
                    ],
                    num: [
                        {required: true, message: '请输入学号', trigger: 'blur'}
                    ],
                },
                rule_tea:{
                    school: [
                        {required: true, message: '请选择学校', trigger: 'blur'}
                    ],
                    department: [
                        {required: true, message: '请选择部门', trigger: 'blur'}
                    ],
                    name: [
                        {required: true, message: '请输入姓名', trigger: 'blur'}
                    ],
                    num: [
                        {required: true, message: '请输入工号', trigger: 'blur'}
                    ],
                },
                rule_sch:{
                    country: [
                        {required: true, message: '请选择国家', trigger: 'blur'}
                    ],
                    province: [
                        {required: true, message: '请选择省份', trigger: 'blur'}
                    ],
                    city: [
                        {required: true, message: '请选择城市', trigger: 'blur'}
                    ],
                    name: [
                        {required: true, message: '请输入学校名', trigger: 'blur'}
                    ]
                },
                countryList:[{
                    value: '中国',
                    label: '中国'
                }],
                provinceList:[{
                    value: '上海',
                    label: '上海'
                }],
                cityList:[{
                    value: '上海',
                    label: '上海'
                }],
                // rules: {
                //     username: [
                //         {required: true, message: '请输入用户名', trigger: 'blur'}
                //     ],
                //     password: [
                //         {required: true, message: '请输入密码', trigger: 'blur'}
                //     ]
                // }
            }
        },
        created() {
            localStorage.clear()
        },
        // directives:{
        //     enterToNext:{
        //
        //     }
        // },
        mounted() {
            let api = this.$api.userApi.listSchool;
            this.axios(api).then(response=>{
                // console.log(response);
                this.schoolList = response.data.data;
            })
        },
        watch:{
            radioT(val) {
                if(this.radioT === 3){
                    document.getElementById("student").style.display="";
                    document.getElementById("teacher").style.display="none";
                    document.getElementById("school").style.display="none";
                }
                else if(this.radioT === 6){
//                    this.axios(api).then(response=>{
//                        // console.log(response);
//                        this.schoolList = response.data.data;
//                    })
                    document.getElementById("student").style.display="none";
                    document.getElementById("teacher").style.display="";
                    document.getElementById("school").style.display="none";
                }
                else{
                    document.getElementById("student").style.display="none";
                    document.getElementById("teacher").style.display="none";
                    document.getElementById("school").style.display="";
                }
            },
            stu_select_schoolS(val) {
                this.ruleForm_Stu.class = '';
                let api = this.$api.userApi.findClassBySchool;
                api.data = {
                    SCHOOL_ID: this.stu_select_schoolS
                }
                this.axios(api).then(response=>{
//                     console.log(response);
                    this.classList = response.data.data;
                })
            },
            stu_select_schoolT(val) {
                this.ruleForm_Tea.department = '';
                let api = this.$api.userApi.findDepartmentBySchool;
                api.data = {
                    SCHOOL_ID: this.stu_select_schoolT
                }
                this.axios(api).then(response=>{
//                    console.log(response);
                    this.departmentList = response.data.data;
                })
            }
//                let api2 = this.$api.userApi.getCourseStu;
//                api2.data={
//                    COURSE_ID: this.select_course
//                };
//                this.axios(api2).then(response=>{
//                    console.log(response);
//                    this.studentTable=response.data.data;
//                });
        },
        methods: {
            studentR(){
                if(this.radioT !== 3 && this.radioT !== 6 && this.radioT !== 9){
                    this.$notify.error({
                        title: '错误',
                        message: '请选择身份'
                    });
                    return;
                }
                else if(this.ruleForm.username ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入用户名'
                    });
                    return;
                }
                else if(this.ruleForm.password ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入密码'
                    });
                    return;
                }

                let apiR = this.$api.userApi.register;
                apiR.data = {
                    username: this.ruleForm.username,
                    password: md5(this.ruleForm.password)
                };
                this.axios(apiR).then(response => {
                    if (response.data.code === 0) {
//                        localStorage.setItem('username', this.ruleForm.username);
                        localStorage.setItem('id',response.data.data);


                        let api = this.$api.userApi.addStudent;
                        api.data = {
                            CLASS_ID:this.ruleForm_Stu.class,
                            STUDENT_NAME:this.ruleForm_Stu.name,
                            STUDENT_NUM:this.ruleForm_Stu.num,
                            USER_ID:localStorage.getItem('id')
                        };
                        this.axios(api).then(response=>{
                            if(response.data.code===0){
                                this.$notify({
                                    title: '成功',
                                    message: '注册成功',
                                    type: 'success'
                                });
                                this.$router.push('/');
                            }else{
                                this.$notify.error({
                                    title: '失败',
                                    message: '信息上传失败'
                                });
                            }
                        })

                    } else if (response.data.code === 1) {
                        this.$message.error('用户名已存在');
                        this.ruleForm.username = '';
                        this.ruleForm.password = ''
                    }
                })
            },

            teacherR(){
//                console.log(this.ruleForm);
//                console.log(this.ruleForm_Stu);
                if(this.radioT !== 3 && this.radioT !== 6 && this.radioT !== 9){
                    this.$notify.error({
                        title: '错误',
                        message: '请选择身份'
                    });
                    return;
                }
                else if(this.ruleForm.username ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入用户名'
                    });
                    return;
                }
                else if(this.ruleForm.password ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入密码'
                    });
                    return;
                }

                let apiR = this.$api.userApi.register;
                apiR.data = {
                    username: this.ruleForm.username,
                    password: md5(this.ruleForm.password)
                };
                this.axios(apiR).then(response => {
                    // console.log(response)
                    if (response.data.code === 0) {
//                        localStorage.setItem('username', this.ruleForm.username);
                        localStorage.setItem('id',response.data.data);


                        let api = this.$api.userApi.addTeacher;
                        api.data = {
                            DEPARTMENT_ID: this.ruleForm_Tea.department,
                            TEACHER_NAME: this.ruleForm_Tea.name,
                            TEACHER_NUM: this.ruleForm_Tea.num,
                            USER_ID: localStorage.getItem('id')
                        };
                        this.axios(api).then(response=>{
//                            console.log(response);
                            if(response.data.code===0){
                                this.$notify({
                                    title: '成功',
                                    message: '注册成功',
                                    type: 'success'
                                });
                                this.$router.push('/');
                            }else{
                                this.$notify.error({
                                    title: '失败',
                                    message: '信息上传失败'
                                });
                            }
                        })

                    } else if (response.data.code === 1) {
                        this.$message.error('用户名已存在');
                        this.ruleForm.username = '';
                        this.ruleForm.password = ''
                    }
                })
            },

            schoolR(){
                // console.log(this.ruleForm);
                // console.log(this.ruleForm_Sch);
                if(this.radioT !== 3 && this.radioT !== 6 && this.radioT !== 9){
                    this.$notify.error({
                        title: '错误',
                        message: '请选择身份'
                    });
                    return;
                }
                else if(this.ruleForm.username ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入用户名'
                    });
                    return;
                }
                else if(this.ruleForm.password ===''){
                    this.$notify.error({
                        title: '错误',
                        message: '请输入密码'
                    });
                    return;
                }

                let apiR = this.$api.userApi.register;
                apiR.data = {
                    username: this.ruleForm.username,
                    password: md5(this.ruleForm.password)
                };
                this.axios(apiR).then(response => {
                    // console.log(response)
                    if (response.data.code === 0) {
//                        localStorage.setItem('username', this.ruleForm.username);
                        localStorage.setItem('id',response.data.data);

                        let api = this.$api.userApi.addSchool;
                        api.data = {
                            country: this.ruleForm_Sch.country,
                            province: this.ruleForm_Sch.province,
                            city: this.ruleForm_Sch.city,
                            schoolname:this.ruleForm_Sch.name,
                            USER_ID: localStorage.getItem('id')
                        };
                        this.axios(api).then(response=>{
//                            console.log(response);
                            if(response.data.code===0){
                                this.$notify({
                                    title: '成功',
                                    message: '注册成功',
                                    type: 'success'
                                });
                                this.$router.push('/');
                            }else{
                                this.$notify.error({
                                    title: '失败',
                                    message: '信息上传失败'
                                });
                            }
                        })

                    } else if (response.data.code === 1) {
                        this.$message.error('用户名已存在');
                        this.ruleForm.username = '';
                        this.ruleForm.password = ''
                    }
                })
            },
        }
    }
</script>

<style scoped>
    .login-wrap {
        position: relative;
        width: 100%;
        height: 100%;
        background-image: url(../../assets/img/login-bg.jpg);
        background-size: 100%;
        background-repeat: no-repeat;
    }

    .ms-title {
        width: 100%;
        line-height: 50px;
        text-align: center;
        font-size: 20px;
        /*color: #fff;*/
        border-bottom: 1px solid #ddd;
    }

    .ms-login {
        width: 40%;
        border-radius: 5px;
        background: rgba(255, 255, 255, 0.8);
        overflow: hidden;
        /*text-align: center;*/
        margin: 0 auto;
        position: relative;
        top: 30px;
    }

    .ms-content {
        padding: 30px 30px;
    }

    .demo-ruleForm{
        margin-top: 40px;
        margin-left: 5px;
    }

    .el-input{
        width: 40%;
    }

    .el-select{
        width: 40%;
    }

    .login-btn {
        text-align: center;
    }

    .login-btn button {
        width: 100%;
        height: 36px;
        margin-bottom: 10px;
    }

    .login-tips {
        font-size: 12px;
        line-height: 30px;
        color: #fff;
    }
    @media screen and (max-width: 1169px){
        .login-wrap{
            background: #6495ED none;
        }
        .ms-login{
            width: 80%;
            top: 50px;
        }
        .ms-content{
            padding: 10px 0px;
        }
        .el-input{
            width: 80%;
        }
        .el-select{
            width: 80%;
        }
    }
</style>
