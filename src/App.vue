<template>
  <v-app>
    <v-content class="grey lighten-4">
      <v-container
        class = "fill-height"
        fluid
      >
        <v-snackbar
          v-model="snackbar"
          :color="snackbarColor"
          :timeout="timeout"
          top
      >
        {{ snackbarText }}
        <v-btn
          dark
          text
          @click="snackbar = false"
        >
          Закрыть
        </v-btn>
        </v-snackbar>
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <v-card class="elevation-12">

              <v-card-title 
                class="grey lighten-2"
              >
                <h1 class="font-weight-bold headline red--text text--darken-4">
                  SCHEME
                </h1>
              </v-card-title>

              <v-tabs
                v-model="tab"
                background-color="grey lighten-4"
                :color="tabColor[tab]"
                centered
                grow
              >

                <v-tab
                  href="#login"
                  class="text-capitalize"
                >
                  {{ tabText.login }}
                </v-tab>

                <v-tab
                  href="#signup"
                  class="text-capitalize"
                >
                  {{ tabText.signup }}
                </v-tab>

                <v-tab-item
                  value="login"
                >
                  <v-card-text>

                    <v-form
                      ref="loginForm"
                      v-model="validLogin"
                      lazy-validation
                    >
                      <v-text-field
                        v-model="email"
                        :rules="emailRules"
                        label="Ваш адрес эл. почты"
                        prepend-icon="mdi-account"
                        type="email"
                        required
                      ></v-text-field>

                      <v-text-field
                        v-model="loginPassword"
                        :rules="passRules"
                        label="Пароль"
                        prepend-icon="mdi-lock"
                        type="password"
                        required
                      ></v-text-field>

                      <v-btn
                        text
                        color="primary"
                      >
                        <span class="text-capitalize">Забыли&nbsp;</span>
                        <span class="text-lowercase">пароль</span>?
                      </v-btn>

                    </v-form>

                  </v-card-text>
                </v-tab-item>

                <v-tab-item
                  value="signup"
                >
                  <v-card-text>

                    <v-form
                      ref="signupForm"
                      v-model="validSignup"
                      lazy-validation
                    >
                      <v-text-field
                        v-model="email"
                        :rules="emailRules"
                        label="Ваш адрес эл. почты"
                        prepend-icon="mdi-account"
                        type="email"
                        required
                      ></v-text-field>

                      <v-text-field
                        v-model="signupPassword"
                        :rules="passSignRules"
                        label="Пароль"
                        prepend-icon="mdi-lock"
                        type="password"
                        required
                      ></v-text-field>

                      <v-text-field
                        v-model="passwordRepeat"
                        :rules="passRepeatRules"
                        label="Повторите пароль"
                        prepend-icon="mdi-lock"
                        type="password"
                        required
                      ></v-text-field>

                      <v-checkbox
                        v-model="privatePolicy"
                      >
                        <template v-slot:label>
                          <div>
                            Я прочитал и согласен с условиями
                            <v-dialog
                              v-model="dialog"
                              width="500"
                            >
                              <template v-slot:activator="{ on }">
                                <span
                                  id="privacy-policy"
                                  v-on="on"
                                  class="text-underline"
                                >
                                  пользовательского соглашения.
                                </span>
                              </template>

                              <v-card>
                                <v-card-title
                                  class="headline grey lighten-2"
                                  primary-title
                                >
                                  Политика конфиденциальности
                                </v-card-title>

                                <v-card-text>
                                  <br>
                                  <ol>
                                    <li>Термин “личная информация”, используемый в настоящем документе, определяется как любая информация, которая идентифицирует или может использоваться для идентификации, связи или поиска человека, к которому такая информация относится. Личная информация, которую мы собираем, будет являться предметом настоящей политики конфиденциальности, с вносимыми время от времени поправками.</li>
                                    <li>Мы не запрашиваем Ваш адрес электронной почты, телефон или какую нибудь информацию о Вас.</li>
                                    <li>Мы не продаем контент.</li>
                                    <li>Мы не требуем регистрации.</li>
                                    <li>Безопасность Вашей персональной информации не будет нарушена.</li>
                                    <li>Мы не просим информацию о местоположении через наше мобильное приложение.</li>
                                    <li>Мы не отправляем на электронную почту рассылку новостей.</li>
                                  </ol>
                                  <br>
                                  <h3>Требуемые разрешения</h3>
                                  <ol>
                                      <li>Доступ к звонкам используется для таких-то целей (укажите для каких).</li>
                                      <li>Доступ к контактам телефона используется для таких то целей (укажите для каких).</li>
                                  </ol>
                                  <br>
                                  <h4>Контакты</h4>
                                  <p>e-mail: <a href="mailto:3dscheme@gmail.com">3dscheme@gmail.com</a></p>
                                </v-card-text>

                                <v-divider></v-divider>

                                <v-card-actions>
                                  <v-spacer></v-spacer>
                                  <v-btn
                                    color="primary"
                                    text
                                    @click="dialog = false"
                                  >
                                    ОК
                                  </v-btn>
                                </v-card-actions>
                              </v-card>
                            </v-dialog>
                          </div>
                        </template>

                      </v-checkbox>

                    </v-form>

                  </v-card-text>
                </v-tab-item>
              </v-tabs>

              <v-card-actions>
                
                <v-container>
                  <v-row
                    align="center"
                    justify="center"
                  >
                    <v-col>

                      <v-btn
                        color="#4285F4"
                        dark
                        small
                        tile
                        depressed
                        @click="googleLogin"
                      >
                        <v-icon left>mdi-google</v-icon>
                        <span class="text-capitalize">{{ tabText.login }}&nbsp;</span>
                        <span class="text-lowercase">с помощью&nbsp;</span>
                        <span class="text-capitalize">google</span>
                        <v-icon right>mdi-chevron-right</v-icon>
                      </v-btn>

                    </v-col>
                  </v-row>
                  <v-row
                    
                  >
                    <v-col>

                      <v-btn
                        color="#4267B2"
                        dark
                        small
                        tile
                        depressed
                        @click="facebookLogin"
                      >
                        <v-icon left>mdi-facebook</v-icon>
                        <span class="text-capitalize">{{ tabText.login }}&nbsp;</span>
                        <span class="text-lowercase">с помощью&nbsp;</span>
                        <span class="text-capitalize">facebook</span>
                        <v-icon right>mdi-chevron-right</v-icon>
                      </v-btn>

                    </v-col>
                  </v-row>
                </v-container>
              </v-card-actions>
                
              <v-btn
                tile
                x-large
                depressed
                block
                :color="tabColor[tab]"
                :loading="loading"
                @click="btnAction[tab]()"
              >
                {{ tabText[tab] }}
                <v-icon right>{{ btnIcon[tab] }}</v-icon>
              </v-btn>

            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data: () => ({
    dialog: false,
    snackbar: false,
    snackbarText: '',
    snackbarColor: 'info',
    timeout: 6000,
    validLogin: true,
    validSignup: true,
    tab: null,
    tabColor: {
      login: 'primary',
      signup: 'success'
    },
    tabText: {
      login: 'Войти',
      signup: 'Зарегистрироваться'
    },
    btnIcon: {
      login: 'mdi-login',
      signup: 'mdi-pencil'
    },
    loading: false,
    email: '',
    loginPassword: '',
    signupPassword: '',
    passwordRepeat: '',
    privatePolicy: false,
    emailRules: [
      v => !!v || 'Необходимо ввести адрес эл. почты',
      v => /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(v) || 'Недопустимый адрес эл. почты',
    ],
    passRules: [ v => !!v || 'Необходимо ввести пароль' ]
  }),
  computed: {
    passSignRules() {
      return [
        ...this.passRules,
        v => !(/\s/.test(v)) || 'Пароль содержит пробельный символ',
        v => /^[a-zA-z0-9!@#$%^&\-_~*+=]+$/.test(v) || 'Пароль содержит недопустимые символы',
        v => /[a-z]/.test(v) || 'Пароль должен содержать минимум одну латинскую букву в нижнем регистре',
        v => /[A-Z]/.test(v) || 'Пароль должен содержать минимум одну латинскую букву в верхнем регистре',
        v => /[0-9]/.test(v) || 'Пароль должен содержать минимум одну цифру',
        v => /[!@#$%^&\-_~*+=]/.test(v) || 'Пароль должен содержать минимум один спец. символ: ! @ # $ % ^ & - _ ~ * + =',
        v => v.length >= 8 || 'Пароль должен быть не менее 8 символов',
        v => v.length <= 32 || 'Пароль должен быть не более 32 символов'
      ]
    },
    passRepeatRules() {
      return [
        v => !!v || 'Введите пароль еще раз',
        v => v === this.signupPassword || 'Пароль не совпадает с введенным выше'
      ]
    },
    btnAction() {
      return {
        login: this.validateLogin,
        signup: this.validateSignup
      }
    }
  },
  methods: {
    validateLogin() {
      if (this.$refs.loginForm.validate()) {
        this.loading = true
        axios.post('/login', {
          email: this.email,
          password: this.loginPassword
        })
        .then(response => {
          this.snackbarText = 'Успешная аутентификация'
          this.snackbarColor = 'success'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ response })
        })
        .catch(error => {
          this.snackbarText = error.message ? error.message : 'Basic error text'
          this.snackbarColor = 'error'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ error })
        })
        setTimeout(() => this.loading = false, 3000)
      }
    },
    validateSignup() {
      if (this.$refs.signupForm.validate()) {
        this.loading = true
        axios.post('/register', {
          email: this.email,
          password: this.signupPassword
        })
        .then(response => {
          this.snackbarText = 'Успешная аутентификация'
          this.snackbarColor = 'success'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ response })
        })
        .catch(error => {
          this.snackbarText = error.message ? error.message : 'Basic error text'
          this.snackbarColor = 'error'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ error })
        })
        setTimeout(() => this.loading = false, 3000)
      }
    },
    googleLogin() {
      axios.get('/google')
        .then(response => {
          this.snackbarText = 'Успешная аутентификация'
          this.snackbarColor = 'success'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ response })
        })
        .catch(error => {
          this.snackbarText = error.message ? error.message : 'Basic error text'
          this.snackbarColor = 'error'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ error })
        })
    },
    facebookLogin() {
      axios.get('/facebook')
        .then(response => {
          this.snackbarText = 'Успешная аутентификация'
          this.snackbarColor = 'success'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ response })
        })
        .catch(error => {
          this.snackbarText = error.message ? error.message : 'Basic error text'
          this.snackbarColor = 'error'
          this.snackbar = true
          // eslint-disable-next-line
          console.log({ error })
        })
    }
  }
}
</script>
<style scoped>
#privacy-policy {
  text-decoration: underline;
}
</style>