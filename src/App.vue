<template>
        <div class="container">
                        <form @submit.prevent="handleSubmit" v-if="!this.success">
                            <div class="line-header">
                                <h2 class="center">Форма для добавления клиента</h2>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="lastName">Фамилия <span>*</span></label>
                                    <input type="text" v-model="formData.lastName" id="lastName" placeholder="Введите фамилию" name="lastName"  :class="{'error-input':submitted && !$v.formData.lastName.required}"/>
                                </div>
                                <div class="line-header">
                                    <div v-if="submitted && !$v.formData.lastName.required" class="invalid-feedback">Фамилия обязательна</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="firstName">Имя <span>*</span></label>
                                    <input type="text" v-model="formData.firstName" placeholder="Введите имя" id="firstName" name="firstName" :class="{'error-input':submitted && !$v.formData.firstName.required}"/>
                                </div>
                                <div class="line-header">
                                     <div v-if="submitted && !$v.formData.firstName.required" class="invalid-feedback">Имя обязательно</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="parentName">Отчество</label>
                                    <input type="text" v-model="formData.parentName" placeholder="Введите отчество" id="parentName" name="parentName"   />
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="firstName">Дата рождения <span>*</span></label>
                                    <input type="date" v-model="formData.bith" id="bith" placeholder="Введите дату рождения" name="bith" :class="{'error-input':submitted && !$v.formData.bith.required}" />
                                </div>
                                <div class="line-header">
                                  <div v-if="submitted && !$v.formData.bith.required" class="invalid-feedback">Дата рождения обязательна</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="firstName">Номер телефона <span>*</span></label>
                                    <input type="text" v-model="formData.phone" id="phone" placeholder="Введите телефон" name="phone"  :class="{'error-input':submitted && (!$v.formData.phone.required || !$v.formData.phone.minLength || !$v.formData.phone.maxLength || !$v.formData.phone.isPhone )}"/>
                                </div>
                                <div class="line-header">
                                    <div v-if="submitted && !$v.formData.phone.required" class="invalid-feedback">Телефон обязателен</div>
                                    <div v-if="submitted && !$v.formData.phone.minLength && $v.formData.phone.isPhone" class="invalid-feedback">Телефон из 11 символов</div>
                                    <div v-if="submitted && !$v.formData.phone.maxLength && $v.formData.phone.isPhone" class="invalid-feedback">Телефон из 11 символов</div>
                                    <div v-if="submitted && !$v.formData.phone.isPhone && $v.formData.phone.required" class="invalid-feedback">Телефон начинается с 7</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-gender">
                                    <label for="firstName" class="label-gender">Пол</label>
                                    <div class="gender">
                                        <input type="radio" v-model="formData.gender" id="male" name="gender" value="мужской" class="form-control" />
                                        <label for="male" class="label-gender">Мужской</label>
                                        <input type="radio" v-model="formData.gender" id="female" name="gender" value="женский" class="form-control" />
                                        <label for="female" class="label-gender">Женский</label>
                                    </div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-header">
                                    <select v-model="formData.client" multiple :class="{'error-input':submitted && !$v.formData.client.required}">
                                        <option disabled value="">Выберите группу клиента *</option>
                                            <option>VIP</option>
                                            <option>Проблемные</option>
                                            <option>ОМС</option>
                                    </select>
                                </div>
                                <div class="line-header">
                                    <div v-if="submitted && !$v.formData.client.required" class="invalid-feedback">Группа клиентов обязательна</div>
                                </div>
                            </div>
                           <div class="form-group">
                               <div class="line-header">
                                    <select v-model="formData.doctor">
                                        <option disabled value="">Выберите лечащего врача</option>
                                            <option>Иванов</option>
                                            <option>Захаров</option>
                                            <option>Чернышева</option>
                                    </select>
                               </div>
                            </div>
                            <div class="form-group">
                                <div class="line-header">
                                    <input type="checkbox" id="sendSms" name="sendSms" v-model="formData.sms" class="form-control">
                                    <label for="sendSms" class="form-control">Не отправлять СМС</label>
                                </div>
                            </div>
                            <hr>
                            <div class="line-header">
                                <h3>Адрес:</h3>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="index">Индекс</label>  
                                    <input type="text" placeholder="Введите индекс" v-model="formData.adress.index" id="index">
                                </div>
                            </div>
                             <div class="form-group">
                                 <div class="line-input">
                                    <label for="country">Страна</label>  
                                    <input type="text" placeholder="Введите страну" v-model="formData.adress.country" id="country">
                                 </div>
                            </div>
                             <div class="form-group">
                                 <div class="line-input">
                                    <label for="state">Область</label>  
                                    <input type="text" placeholder="Введите область" v-model="formData.adress.state" id="state">
                                 </div>
                            </div>
                             <div class="form-group">
                                 <div class="line-input">
                                    <label for="city">Город <span>*</span></label>  
                                    <input type="text" placeholder="Введите город" v-model="formData.adress.city" id="city" :class="{'error-input':submitted && !$v.formData.adress.city.required}"> 
                                 </div>  
                                 <div class="line-header">                          
                                    <div v-if="submitted && !$v.formData.adress.city.required" class="invalid-feedback">Город обязателен</div>
                                 </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="street">Улица</label>  
                                    <input type="text" placeholder="Введите улицу" v-model="formData.adress.street" id="street">
                                </div>
                            </div>
                             <div class="form-group">
                                 <div class="line-input">
                                    <label for="home">Дом</label>  
                                    <input type="text" placeholder="Введите дом" v-model="formData.adress.home" id="home">
                                 </div>
                            </div>
                            <hr>
                            <div class="line-header">
                                <h3>Паспорт:</h3>
                            </div>                            
                            <div class="form-group">
                                <div class="line-header">
                                    <select v-model="formData.document.type" :class="{'error-input':submitted && !$v.formData.document.type.required}">
                                        <option disabled value="">Выберите вид документа </option>
                                            <option>Паспорт</option>
                                            <option>Свидетельство о рождении</option>
                                            <option>Вод. удостоверение</option>
                                    </select>
                                </div>
                                <div class="line-header">
                                    <div v-if="submitted && !$v.formData.document.type.required" class="invalid-feedback">Тип документа обязателен</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="seria">Серия</label>  
                                    <input type="text" placeholder="Введите серию" v-model="formData.document.seria" id="seria">
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="number">Номер</label>  
                                    <input type="text" placeholder="Введите номер" v-model="formData.document.number" id="number">
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="issuedBy">Кем выдан</label>  
                                    <input type="text" placeholder="Введите кем выдан" v-model="formData.document.issuedBy" id="issuedBy">
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-input">
                                    <label for="dateIssue">Дата выдачи <span>*</span></label>  
                                    <input type="date" placeholder="Введите дату выдачи" v-model="formData.document.dateIssue" id="dateIssue" :class="{'error-input':submitted && !$v.formData.document.dateIssue.required}">
                                </div>   
                                <div class="line-header"> 
                                    <div v-if="submitted && !$v.formData.document.dateIssue.required" class="invalid-feedback">Дата выдачи обязательна</div>
                                </div>
                            </div>
                            <div class="form-group">
                                <div class="line-header"> 
                                  <button type="submit" class="btn btn-primary">Зарегистрировать</button>
                                </div>
                            </div>
                        </form>
    <div class="message" v-else>
        <h1 class="center add-user">Пользователь успешно добавлен</h1>
        <div class="line-header">       
            <button @click="clickHandler">Добавить еще</button>
        </div>
    </div>
    </div>
</template>

<script>
    import { required, minLength, maxLength } from "vuelidate/lib/validators";
    import { isPhone } from "@/validators/validators";
    export default {
        name: "app",
        data() {
            return {
                formData: {
                    firstName: "",
                    parentName:"",
                    lastName: "",
                    bith:"",
                    gender:[],
                    client:[],
                    doctor:'',
                    sms:false,
                    phone:"",
                    adress:{
                        index:'',
                        country:'',
                        state:'',
                        city:'',
                        street:'',
                        home:''

                    },
                    document:{
                        type:'',
                        seria:'',
                        number:'',
                        issuedBy:'',
                        dateIssue:''
                    }
                },
                submitted: false,
                success: false
            };
        },
        validations: {
            formData: {
                firstName: { required },
                lastName: { required },
                bith:{required},
                client:{required},
                phone:{required,minLength:minLength(11),maxLength:maxLength(11),isPhone},
                adress:{
                    city:{required}
                },
                document:{
                    type:{required},
                    dateIssue:{required}
                }
                }
        },
        methods: {
            handleSubmit() {
                this.submitted = true;
                this.$v.$touch();
                if (this.$v.$invalid) {
                    return;
                }
            this.success = true;
                
            },
            clickHandler(){
              this.success = false;
              this.clear();
            },
            clear(){
                this.submitted = false;
                this.formData.firstName = '';
                this.formData.parentName = '';
                this.formData.lastName = '';
                this.formData.bith = '';
                this.formData.gender = [];
                this.formData.client = [];
                this.formData.doctor = '';
                this.formData.sms = false;
                this.formData.phone = '';
                this.formData.adress.index = '';
                this.formData.adress.country = '';
                this.formData.adress.state = '';   
                this.formData.adress.city = '';    
                this.formData.adress.street = '';    
                this.formData.adress.home = '';   
                this.formData.document.type = '';   
                this.formData.document.seria = '';     
                this.formData.document.number = '';    
                this.formData.document.issuedBy = '';    
                this.formData.document.dateIssue = '';   
               
                
            }
        }
    };
</script>
<style lang="sass" scoped>
$color: black;
label
  padding: 0
  margin: 0
  height: fit-content
.form-group 
  color: $color;

.container
  display: flex
  justify-content: center
  width: 100%

.line-input
  margin: 5px 0
  width: 100%
  display: flex
  justify-content: space-between
  align-items: center
.line-header
  margin: 5px 0
  width: 100%
  display: flex
  justify-content: center
form
  padding: 20 0
button
  padding: 15px 40px
  size: 20px
  font-weight: bold
  border-radius: 10px
  background-color: blue
  color: white
  margin: 20px 0
input
  width: 60%
button:hover
  cursor: pointer
label
  width: 40%
.form-control
 width: fit-content
.invalid-feedback
  color: red
.label-gender
  width: fit-content
.line-gender
   display: flex
   justify-content: center
.center
 text-align: center
label
 span
  color: red
form
  border: blue solid 2px
  padding: 10px 20px
  border-radius: 20px
hr
  border-color: blue 
  margin-top: 20px
.error-input
  border-color: red
.error-input:focus
  box-shadow: red 0.2px 0.2px 6px 1px
  outline-style: none
.message
  position: absolute
  top: 20%
  rigth 50%
  height: 400px
  width: 40%
  background-color: white 
.add-user
  margin-top: 2em
</style>