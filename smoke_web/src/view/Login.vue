<template>
    <div class="flex  justify-start  h-screen bg-[#7300ff] m-28 rounded-2xl ">
        <div class=" items-center p-28">

            <div class="bg-white rounded-full p-56 ">
                <h1 class=" text-black font-black ">Logo</h1>
            </div>
        </div>
        <div class="w-1/3 pt-36 ">
            <h1 class="text-3xl font-bold mb-6 ">เข้าสู่ระบบ</h1>
            <form @submit.prevent="userLogin">
                <div class="mb-4">

                    <label for="email" class="block mb-2">
                        Email
                    </label>
                    <input type="email" v-model="email" id="email" placeholder="กรุณาป้อนอีเมล"
                        class="w-full px-4 py-2 border rounded text- " />
                </div>
                <div class="mb-4">
                    <label for="password" class="block mb-2">
                        Password
                    </label>
                    <input type="password" v-model="password" id="password" placeholder="กรุณาป้อนรหัสผ่าน"
                        class="w-full px-4 py-2 border rounded " />

                </div>

                <button type="submit" class="bg-green-500 text-white w-full py-2 rounded">
                    Login
                </button>
            </form>
        </div>

    </div>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2';

export default
    {
        name: 'Login',
        data() {
            return {
         
                email: '',   // Capture email input
                password: '', // Capture password input
                role: '',     // Capture role input
            };
        },
        methods: {
            async userLogin() {
                try {
                    const response = await axios.post('http://localhost:5000/users/login', {
                        email: this.email,
                        password: this.password,
                    });
                    console.log(response.data);
                    localStorage.setItem('userToken', response.data.token);
                    localStorage.setItem('userToken', response.data.token);
                    localStorage.setItem('username', response.data.username);
                    localStorage.setItem('role', JSON.stringify(response.data.role));
                    localStorage.setItem('_id', response.data._id);
                    console.log(localStorage.getItem('_id'));

                    // alert('User logged in successfully');

                    // console.log(typeof (localStorage.getItem('role')));
                    const user = JSON.parse(localStorage.getItem('role'));
                    
                    // console.log(user);
                    console.log('admin' == user);
                    console.log(response.data);
                  

                    
                    Swal.fire({
                        icon: 'success',
                        title: 'Logged in successfully',
                        showConfirmButton: false,
                        timer: 1500
                    });
                    if (user == 'admin') {
                        this.$router.push({ name: 'ChangeUser' });
                    } else {
                        console.log(user);
                        this.$router.push({ name: 'Home' });
                    }
                    // this.$router.push({ name: 'Home' });
                } catch (err) {
                    console.error(err);

                    Swal.fire({
                        title: 'Error!',
                        text: 'Invalid email or password',
                        icon: 'error',
                        confirmButtonText: 'OK!'
                    })
                }
            },



        },
        
    }



</script>

<style>
/* Add any custom styles here */
</style>