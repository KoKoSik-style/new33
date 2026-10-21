<template>
  <div class="page center">
    <h2>Вход</h2>
    <form @submit.prevent="login">
      <input v-model="password" type="password" placeholder="Пароль (введите 'demo')" />
      <button type="submit">Войти</button>
    </form>
    <p v-if="error" style="color: red; margin-top: 0.5rem;">
      {{ error }}
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import {useRouter } from 'vue-router'

// Переменная для хранения введенного пароля
const password = ref('')

// Переменная для хранения текста ошибки (изначально ошибки нет)
const error = ref(null)

// Получаем доступ к роутеру для перенаправления пользователя
const router = useRouter()


// 3. логика авторизации 
const login = () => {
  error.value = null
  
  // Проверяем, совпадает ли введенный пароль с 'demo'
  if (password.value === 'demo') {
    // Если пароль верный:
    localStorage.setItem('token', 'demo') // Сохраняем токен в браузере
    router.push({ name: 'Dashboard' })    // Переходим на защищенную страницу
  } else {
    // Если пароль неверный:
    error.value = 'Неверный пароль. Попробуйте "demo"' // Показываем ошибку
  }
}
</script>

<style scoped>
.center { text-align: center; }
input { padding: 0.5rem; margin-right: 0.5rem; }
button { padding: 0.5rem 1rem; }
</style>