<template>
    <div>
        <h2>Form Projesi</h2>

        <!--Form Uzerindeki Data lari Gonderme Isleminden Sonra
            Sayfada Yenileme Islemini Durdurmak Icin
            prevent Kullaniyoruz-->
        <form @submit.prevent="handleSubmit()">
            <label>Email:</label>

            <!--Input Elementi Icine Girilen Degeri
                v-model Property Icinde Yazilan Property ile
                script Icinde Yer Alan Data Alani Icinde 
                Ilgili Property e Gondererek
                Yapilacak Islem Surecini Baslatiyoruz-->
            <input type="email" v-model="email" required>
            <label>Şifre:</label>
            <input type="password" v-model="password" required>

            <!--Password Girilirken Hata Olursa Kullaniciya Gorunecek Satir-->
            <div class="error" v-if="passwordError">
                {{passwordError}}
            </div>
            <label>Cinsiyet:</label>
            <select v-model="gender">    
                <option value="male">Erkek</option>
                <option value="female">Kadın</option>
            </select>
            <label>Bildiğiniz Diller</label>

            <!--keyup Event Kullanilarak Input Element Icine Girilen Data yi
                addSkill Metodu Uzerinden 
                Property Olarak Kullanilan 
                skills Array Icine Aliyoruz-->
            <input type="text" v-model="skill" @keyup.alt="addSkill($event)">

            <!--skills Array Icinde Yer Alan Data lari Yazdirmak Icin
                skills Array Icinde Tarama Yapiyoruz
                Tarama Sonucunu skillItem Degiskeni Uzerinden Yazdiriyoruz-->
            <div v-for="skillItem in skills" :key="skillItem" class="skillItem">

                <!--Ekarana Yazdirilan Data lari Uzerine Tiklandiginda
                    Silinebilir Hale Getiriyoruz-->
                <span @click="deleteSkill(skillItem)">{{skillItem}}</span>
            </div>
            <div class="term">

                <!--Checkbox Elementi Icinde Degerin Secilme Durumunu
                    v-model Property Icinde Yazilan Property ile
                    script Icinde Yer Alan Data Alani Icinde 
                    Ilgili Property e Gondererek
                    Yapilacak Islem Surecini Baslatiyoruz-->
                <input class="termInput" v-model="term" type="checkbox" required>
                <label>Kullanım koşullarını kabul ediniz</label>
            </div>
            <div class="btnDiv">
                <button>Kaydol</button>
            </div>
        </form>
        <!-- 
            <p>{{email}}</p>
            <p>{{password}}</p>
            <p>{{gender}}</p>
            <p>{{term}}</p> 
        -->
    </div>
</template>

<script>

export default {
    data() {
        return {
            email:'ccc@hotmail.com',
            password:'',
            gender:'male',
            term:false,
            skill:'',
            skills:[] ,
            passwordError:null          
        }
    },
    methods: {
        addSkill(event)
        {
            // Input Icine Girilen Data yi Yazdirmak Icin
            // , Karakterini Girmek Gerekiyor
            if(event.key === ',' && this.skill)
            {

                // Girilen Data Daha Once Girildi Kontrol Ediyoruz
                // Girildi Ise Yazdirma Islemini Yapmiyoruz
                // Girilmedi Ise Yazdiriyoruz
                if(!this.skills.includes(this.skill)){
                     this.skills.push(this.skill);
                }               
                  this.skill=''
            }      
        },
        deleteSkill(skill){

            // Ekranda Yazili Olan Data larin Bulundugu Array Icinde Filtreleme Yapiyoruz
            this.skills=this.skills.filter(item =>{

                // Uzerine Tiklanan Data Haricinde Data Var Ise
                // O Data lari Donduruyoruz
                return skill !== item
            })
        },

        // Butona Tiklandiginda Gonderme Islemi Icin
        // Form Uzerinden Alinacak Data lar
        handleSubmit(){

            // Password Girilirken Validation Islemi Yapimi
            this.passwordError = this.password.length > 5 ? '' : 'Lütfen minumum 6 karakterli bir şifre giriniz'
            console.log('Email',this.email)
            console.log('Passsword',this.password)
            console.log('Gender',this.gender)
            console.log('Term',this.term)
            console.log('Skills',this.skills)
        }
    },
}
</script>

<style>
    form{
        max-width: 450px;
        width: 100%;
        background: antiquewhite;
        padding: 40px;
        border-radius: 20px;
        text-align: left;
        margin: 40px auto;
    }
    input,select{
        display: block;
        width: 100%;
        padding: 10px 8px;
        border-radius: 20px;
        border: none;
        outline: none;
    }
    label{
        margin: 15px 10px;
        display: inline-block;
        font-size: 15px;
        font-weight: bold;
        letter-spacing: 2px;
    }
    .termInput{
        width: 16px;
    }
    .term{
        display: flex;
        align-items: center;
    }
    button{
        border: none;
        background: green;
        color: white;
        padding: 10px 20px;
        font-size: 18px;
        border-radius: 20px;
    }
    .skillItem{
        background: white;
        margin: 20px 10px;
        display: inline-block;
        padding: 8px 10px;
        border-radius: 20px;
        color: gray;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    .error{
        color: red;
        letter-spacing: 1px;
        margin-top: 10px;
        font-size: 15px;
        font-weight: bold;
    }
</style>