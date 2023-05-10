<template>
  <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
    <div class="w-screen bg-white flex-col rounded-lg flex justify-center items-center shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
      <h1 class="text-xl my-8 font-bold text-gray-900 md:text-2xl dark:text-white">
        ورود
      </h1>
      <Form class="space-y-4 w-[80%] md:space-y-6" @submit="login" :validation-schema="LoginFormSchema">
        <!-- email input -->
        <div>
          <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">ایمیل</label>
          <Field :validate-on-input="true" type="email" name="email" class="bg-gray-50 border invalid:bg-red-600/70  border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="ایمیل خود را وارد کنید"/>
          <p class="text-red-500 my-2 text-[15px]" >
          <ErrorMessage name="email"/>
          </p>
        </div>

        <!-- password input -->
        <div>
          <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">پسورد</label>
          <Field :validate-on-input="true" type="password" name="password" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="پسورد خود را وارد کنید"/>
          <p class="text-red-500 my-2 text-[15px]">
            <ErrorMessage name="password"/>
          </p>
        </div>

        <!-- check input -->
        <div class="flex w-full justify-between items-start">
            <div class="flex flex-row-reverse">
                <div class="flex items-center h-5">
                <input type="checkbox" class="w-4 h-4 border accent-pink-500 border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-sky-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-sky-600 dark:ring-offset-gray-800">
            </div>

            <div class="ml-3 text-sm">
                <label for="remember" class="text-gray-500 dark:text-gray-300">من را به خاطر بسپار</label>
            </div>
            </div>

            <a href="#" class="text-sm font-medium text-sky-600 hover:underline dark:text-sky-500">رمز خود را فراموش کرده اید</a>
        </div>

        <!-- submit button -->
        <div class="w-full flex justify-center m-0">
            <button type="submit" class="text-white bg-sky-600 hover:bg-sky-700 mb-6 focus:ring-4 focus:outline-none focus:ring-sky-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-sky-600 dark:hover:bg-sky-700 dark:focus:ring-primary-800">ثبت نام</button>
        </div>

      </form>
    </div>
  </div>
</template>


<script setup>
// import reactive  from "vue";
import { Form, Field, ErrorMessage } from "vee-validate";
import { reactive } from "vue";
import { string, object } from "yup";

components: {
  Form;
  Field;
  ErrorMessage;
}

const LoginFormSchema = reactive(
  object({
    email:string().required('ایمیل خود را وارد کنید').email('ایمیل نامعتبر است'),
    password: string().required("پسورد را وارد کنید").min(6, "پسورد باید بیشتر از 6 کارکتر باشد"),
  })
)


function login(values) {
  console.log(values);
}
</script>

<style>

</style>