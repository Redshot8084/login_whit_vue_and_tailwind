<template>
  <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
    <div class="w-screen bg-white flex-col rounded-lg flex justify-center items-center shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
      <h1 class="text-xl my-8 font-bold text-gray-900 md:text-2xl dark:text-white">
        ثبت نام
      </h1>
      <Form class="space-y-4 w-[95%] md:space-y-6" @submit="register"  :validation-schema="RegisterFormSchema">
        <div class="grid grid-cols-1 w-full gap-4 md:grid-cols-2">
          <!-- name input -->
        <div>
          <Field type="name" name="name" :validate-on-input="true" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="نام نام خانوادگی خود را وارد کنید"/>
            <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="name"/></p>
        </div>

          <!-- email input -->
        <div>
          <Field type="email" name="email" :validate-on-input="true" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="ایمیل خود را وارد کنید"/>
          <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="email"/></p>
        </div>

        <!-- password input -->
        <div>
            <Field type="password" name="password" :validate-on-input="true" placeholder="پسورد خود را وارد کنید" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" />
            <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="password"/></p>
        </div>

        <!-- ConfirmPassword input -->
        <div>
            <Field type="password" name="ConfirmPassword" :validate-on-input="true" placeholder="تکرار پسورد خود را وارد کنید" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"/>
            <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="ConfirmPassword"/></p>
        </div>

        <!-- PhoneNumber input -->
        <div>
            <Field type="text" name="PhoneNumber" :validate-on-input="true" placeholder="شماره تلفن خود را وارد کنید" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"/>
            <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="PhoneNumber"/></p>
        </div>

        <!-- rols input -->
        <div>
            <Field as="select" name="rols" :validate-on-input="true" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-sky-600 focus:border-sky-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <option>نقش خود را انتخاب کنید</option>
              <option value="user">کاربر</option>
              <option value="student">دانشجو</option>
              <option value="teacher">مدرس</option>
            </Field>
            <p class="text-red-500 my-2 text-[15px]"><ErrorMessage name="rols"/></p>
        </div>


        <div class="text-white text-base">
          <div class="form-group mt-3" style="text-align: right;">
            <label for="1">آقا</label><Field type="radio" id="1" class="m-2 accent-pink-500" name="gender" value="آقا"/>
            <label for="2">خانوم</label><Field type="radio" id="2" class="m-2 accent-pink-500" name="gender" value="خانوم"/>
            <label for="3">نامشخص</label><Field type="radio" id="3" class="m-2 accent-pink-500" name="gender" value="نامشخص"/>
          </div>
          <p class="text-red-500 my-2 text-[15px]"></p>
        </div>
        </div>


        <!-- submit button -->
        <div class="w-full flex justify-center m-0">
            <button type="submit" class="text-white bg-sky-600 hover:bg-sky-700 mb-6 focus:ring-4 focus:outline-none focus:ring-sky-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-sky-600 dark:hover:bg-sky-700 dark:focus:ring-primary-800">ورود به سایت</button>
        </div>

      </form>
    </div>
  </div>
</template>

<script setup>
import { Form, Field, ErrorMessage } from "vee-validate";
import { reactive } from "vue";
import { string, object  , ref} from "yup";

components: {
  Form;
  Field;
  ErrorMessage;
}


const RegisterFormSchema = reactive(
object({
  name: string().required("نام خود را وارد کنید"),
    email: string().required("ایمیل خود را وارد کنید").email("ایمیل نامعتبر است"),
    password: string().required("پسورد خود را وارد کنید").min(8, "پسورد باید بیش از 8 کلمه باشد"),
    ConfirmPassword: string()
      .required("پسورد را تکرار کنید")
      .oneOf([ref("password")], "پسورد یکسان نیست"),
      PhoneNumber: string()
      .required("شماره تلفن را وارد کنید")
      .min(11, "شماره تلفن باید 11 رقم باشد")
      .max(11, "شماره تلفن باید 11 رقم باشد"),
    rols: string().required("نقش خود را انتخواب کنید"),
    gender : string().required(),
})
)



function register(values) {
  console.log(values);
}
</script>

<style>

</style>