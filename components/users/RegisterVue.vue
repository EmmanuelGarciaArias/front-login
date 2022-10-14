<template>
    <v-row class="renglon">
        <v-col cols="6">
            <v-froms ref="form" v-model="valid">
                <v-card>
                    <v-card-title>
                        Registro de Usuarios
                    </v-card-title>
                    <v-carrt-text>
                        <v-text-field
                        v-model="Usuario"
                        type="text"
                        placeholder="Escribe el Nombre de ususario"
                        label= "Usuario"
                        />
                        <v-text-field
                        v-model="mail"
                        type="mail"
                        :rules="emailRule"
                        placeholder="Escribe el Correo de ususario"
                        label= "Correo Electronico"
                        />
                        <v-text-field
                        v-model="password1"
                        :rules="longPassword"
                        type="password"
                        placeholder="Escribe el Password de ususario"
                        label= "Password"
                        />
                        <v-text-field
                        v-model="password2"
                        :rules="matchingPassword"
                        type="password"
                        placeholder="Verifica la contraseña"
                        label= "Usuario"
                        />
                    </v-carrt-text>
                <v-card-actions>
                    <v-btn 
                    color="green"
                    @click="registraUsuario"
                    >Registrar
                    </v-btn>
                </v-card-actions>
                </v-card>
            </v-froms>
        </v-col>
    </v-row>
</template>

<script>
    export default{
        data (){
            return{
            valid: false,
            name: null,
            mail: mull,
            password1: null,
            password2: null,
            emailRule: [
            v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
                ],
            longPassword:[
                v=>{
                    if(!v || v.length < 6 ){
                        return 'Longitud Invalida'
                    }
                    return true
                }              
            ],
            matchingPassword[ () => {
                if(this.password1 === this.password2){
                    return true
                }else{
                    return 'Password does not match.'
                }
            }]
        }
        },
        methods: {
        async registraUsuario(){
            this.valid = this.$refs.form.validate()
            if(this.valid){
                const headers = {
                    'Content-Type': 'application/json; charset=UTF-8',
                    'Access-Control-Allow-Origin':'*'
                }
                const data={
                    name: this.name,
                    email: this.mail,
                    password: this.password1
                }
                await this.$axios.post('/register',
                data,
                { headers }
                ).then((res)=>{
                    console.log(res)
                }).catch((error)=>{

                })
            }else{
                console.log('invalid')
            }
        }
    }
    }
</script>
<style>
    .renglon{
        width: 100%;
        height: 100%;
        padding: 0;
        margin: 0;
        background-color: bisque;
    }
</style>