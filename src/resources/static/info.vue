<template>
    <div>
        <head>
            <title>个人信息</title>
        </head>
    <body>
        <!-- 顶 (Group) -->
        <el-row><div class="group-bg">
            </br>          
            <!--welcome-->
            <el-col :span="6" :offset="2">
                <div id="welcome">
                    <p><span>Welcome to MoreThings!</span></p>
                </div>
            </el-col>

            <!--首页-->

            <el-col :span="4">
                <div class="btn">
                    <el-button type="text" @click="home">首页</el-button>
                </div>
            </el-col>
            <!--登陆-->
            <el-col :span="4">
                <div class="btn">
                    <el-button type="text" disabled="true">登陆</el-button>
                </div>
            </el-col>
            <!--购物车-->
            <el-col :span="4">
                <div class="btn">
                    <el-button type="text" @click="cart">购物车</el-button>
                </div>
            </el-col>
            <!--我的-->
            <el-col :span="4">
                <div class="btn">
                    <el-dropdown @my="chooseMy">
                        <span class="el-dropdown-link">
                            我的<i class="el-icon-caret-bottom el-icon--right"></i>
                        </span>
                        <el-dropdown-menu slot="dropdown">
                            <el-dropdown-item command="order">订单</el-dropdown-item>
                            <el-dropdown-item disabled>个人信息</el-dropdown-item>
                        </el-dropdown-menu>
                    </el-dropdown>
                </div>
            </el-col> 
             </div>     
        </el-row>

        </br>

        <!--个人资料-->
        <el-row>
            <el-col :span="4">
                <div class="">
                    <el-tag>个人资料</el-tag>
                </div>
            </el-col>
       
        </el-row>

        <div id="info">
            </br>
            <el-form :model="edit" :rules="editRules" ref="edit" label-width="80px" >
                <el-form-item prop="phoneNumber" label="手机号">                                
                    <el-input v-model="edit.phoneNumber" auto-complete="off"></el-input>                               
                </el-form-item>
                <el-form-item prop="nickName" label="昵称">
                    <el-input v-model="edit.nickName" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item prop="password" label="密码">
                    <el-input v-model="edit.password" type="password" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item label="性别">
                    <el-radio class="radio" v-model="edit.radio" label="1">男</el-radio>
                    <el-radio class="radio" v-model="edit.radio" label="2">女</el-radio>
                    </el-form-item>
                <el-form-item label="生日">
                    <el-date-picker v-model="edit.birthDay" type="date" placeholder="选择日期" > </el-date-picker>
                </el-form-item>
                <el-form-item prop="address" label="地址">    
                    <el-input v-model="edit.address" type="address" auto-complete="off"></el-input>
                </el-form-item>
                                       
            </el-form>

            <el-row>
            <!--确认-->
            <el-col :span="2" :offset="17">
                <div id="edit-con" class="btn">
                    <el-button type="info"  @click="edit_con">确认修改</el-button>
                </div>
            </el-col>

            <el-col :span="1" :offset="1">
                <div id="cancel" class="btn">
                    <el-button type="info"  @click="cancel">取消</el-button>
                </div>
            </el-col>
            </el-row>

 </div>


    </body>
    </div>    
</template>
<script>
export default {
    methods:{
        //跳转页面到首页，购物车
        home(){
             this.$router.push({
                path: '/customer/cHome'
            });
        },
        cart(){
            this.$router.push({
                path: '/customer/shoppingCart'
            });
        },
        edit_con(){//如修改成功则有消息提示
            this.$message({
                showClose:true, 
                message:"修改成功！",
            });
        },
        changeMy(my) {
            this.$message('click on item ' + order);
        },   
    },
    data:function(){
       //检测用户输入的手机号码是否为11位
        var checkPhoneNumber =(rule,value,callback)=>{
            if(value.length!=11){
                callback(new Error('手机号码须有11位'));
            }else{
                callback();
            }
        }; 
        //检测密码是否由数字和字母组成
        var checkWord = (rule, value, callback) => { 
                var reg = /^[a-zA-Z0-9]+$/;
                if (value.match(reg)) {
                    callback();
                } else {
                    callback(new Error('密码仅可由数字与字母组成'));
                }
            };
        return{
            edit:{
                phoneNumber:'',
                nickName:'',
                password:'',
                address:'',
                radio:'1',
                birthDay:''
            },
            
        editRules: {
                phoneNumber: [
                        { required: true, message: '手机号码不可为空' }, 
                        { validator: checkPhoneNumber, trigger: 'change' },
                        { validator: checkPhoneNumber, trigger:'blur'}  
                       
                 ],
                 nickName:[
                     { required: true, message:"昵称不可为空" },
                     { required: true, message:"昵称不可为空", trigger:'blur'}
                 ],
                 password:[
                     { required: true, message:"密码不可为空" },
                     { validator: checkWord, trigger: 'change' },
                     { validator: checkWord, trigger: 'blur' }
                 ],
                 address:[
                    { required: true, message:"地址不可为空" },
                    { required: true, message:"地址不可为空", trigger:"blur"},                     
                 ]
             }
        }
    }
}


</script>
<style>
.group-bg {
    background:	#708090;
    margin:0 auto;
    top:0px;
    width:1280px;
    height:90px;
}
#welcome {
    color:white;
}
.btn {
    text-align:center;
}
.el-tag{
    width:90px;
    height:40px;
    margin-left:345px;
    font-size:16px;
    padding:10px 10px 10px 10px;
    color:white;
    background:#20A0FF;
}
#info {
    width:800px;
    height:450px;
    border-width:1px;
    border-style:solid;
    margin:0 auto;
}
.el-input{
    width:650px;
}

</style>
