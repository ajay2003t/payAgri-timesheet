<template>
    <div class="main">
        <header>
            <img src="https://www.payagri.com/assets/images/logo.png" alt="Company Logo" class="logo">
            <h1 class="heading">Timesheet Management</h1>
            <div class="profile-box">
                <img src="../assets/image/user.png" class="profile">
                <p class="profile-text">{{ name }}</p>
            </div>
        </header>

        <div class="container">
            <div class="box" @click="goToWeeklyLog">
                <a><img src="../assets/image/weekly log.png" alt="Image 3" class="img"></a>
                <a class="txt">
                    <h2>Weekly Log</h2>
                </a>
            </div>
            <div class="box" @click="goToCalender">
                <a><img src="../assets/image/my calender.png" alt="Image 4" class="img"></a>
                <a class="txt">
                    <h2>My Calendar</h2>
                </a>
            </div>
            <div class="round" @click="addproject">
                <a><img src="../assets/image/Picsart_24-06-21_15-15-14-566 (2).png" alt="Add Project" class="img1"></a>
            </div>
            <div class="round1" @click="addTask">
                <a><img src="../assets/image/task.png" alt="Add Task" class="img1"></a>
            </div>
        </div>
    </div>
</template>

<script>
import { auth, db } from '@/firebase/firebase';
import { onAuthStateChanged } from 'firebase/auth';
import { doc, getDoc } from 'firebase/firestore';

export default {
    data() {
        return {
            userId: '',
            zId: '',
            name: ''
        };
    },
    mounted() {
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                this.userId = user.uid;
                const docRef = doc(db, 'users', user.uid);
                const docSnap = await getDoc(docRef);
                if (docSnap.exists()) {
                    this.zId = docSnap.data().zId;
                    this.name = docSnap.data().name;
                } else {
                    console.error('No such document!');
                }
            } else {
                this.$router.push('/');
            }
        });
    },
    methods: {
        goToWeeklyLog() {
            if (this.zId) {
                const url = 'https://creatorapp.zohopublic.in/zoho.admin_payagri/timesheet-management/form-perma/Weekly_Logs/UWfECDWhPdzAbSjhh1bq0FHpUnUy5Q1y9zW5hJ2QdkbBFzRZhmk0XtxdBCkSDEYQQ2BpXUBnTUfavGQXJGwVTVES9aHAwTXGwXFz?Employee_Name=' + this.zId + '&Check=true';
                window.open(url, '_blank');
            } else {
                console.error('zId is not available');
            }
        },
        goToCalender() {
            if (this.zId) {
                const url = 'https://creatorapp.zohopublic.in/zoho.admin_payagri/timesheet-management/report-perma/My_Calender/pbF8g2ypMpkjt29gVmjOkN3DKBfA2XpJYCpMQspb3GWKArBm8XyjR3WQKuFT74gn63rwgtsRfA2AgnXAGBBdmy6khqHm3YF4Ahpu?zc_AddRec=false&zc_DelRec=false&zc_ShowAs=false&zc_Search=false&Employee_Name=' + this.zId;
                window.open(url, '_blank');
            } else {
                console.error('zId is not available');
            }
        },
        addproject() {
            if (this.zId) {
                const url = 'https://creatorapp.zohopublic.in/zoho.admin_payagri/timesheet-management/form-perma/Project/dnHfY1sQ99smFnNPWREjGAXFVKgNQReY7uemgmz97u6DhMhFwYqhV6G7fU5e075Wy85sZtfUmnhOCQvuh6zryQ7QXQAVXKHgSjp6?Employee_Name=' + this.zId;
                window.open(url, '_blank');
            } else {
                console.error('zId is not available');
            }
        },
        addTask() {
            if (this.zId) {
                const url = 'https://creatorapp.zohopublic.in/zoho.admin_payagri/timesheet-management/form-perma/Task/t7ENRumHx2N09myDaTCwAfZYnb4GHjnA1XvJBSOaav1GSuNrjdxgrFmAwPqpjeTyGzpzUZzZjvCx3wX0nxV1RS3qyHFkHpJdNMfd?Employee_Name=' + this.zId;
                window.open(url, '_blank');
            } else {
                console.error('zId is not available');
            }
        }
    }
};
</script>

<style scoped>
* {
    background: transparent;
    user-select: none;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    user-select: none;
}

.main {
    min-height: 100vh;
    background-image: linear-gradient(rgba(4, 9, 30, 0.7), rgba(4, 9, 30, 0.7)), url(https://img-s-msn-com.akamaized.net/tenant/amp/entityid/BB1msOP2.img);
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    color: white;
    text-align: center;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5em;
    background-color: rgba(0, 0, 0, 0.5);
}

.logo {
    width: 13vw;
    margin-right: 20px;
}

.heading {
    font-family: 'Trebuchet MS', Arial, sans-serif;
    background-color: transparent;
}

.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1%;
    padding: 6em 1em;
}

.box {
    flex: 0 0 30%;
    max-width: 24%;
    background-color: #ccc;
    margin: 10px;
    border-radius: 20px;
    text-align: center;
    transition: 0.5s;
    padding: 1em;
    box-sizing: border-box;
}

.box:hover {
    transform: scale(1.05);
    opacity: 0.8;
}

.box img {
    max-width: 33%;
    height: auto;
    display: block;
    margin: 0 auto 1em;
}

.box h2 {
    margin: 0;
}

a {
    text-decoration: none;
    color: black;
    cursor: pointer;
}

.round {
    position: absolute;
    right: 0px;
    top: 35%;
    transition: 0.5s;
    padding: 0em;
}

.round1 {
    position: absolute;
    right: 0px;
    top: 52%;
    transition: 0.5s;
    padding: 0em;
}

@media (max-width: 1321px) {
    .round {
        top: 40%;
    }

    .round1 {
        top: 57%;
    }
}

@media (max-width: 768px) {
    .round {
        top: 45%;
    }

    .round1 {
        top: 62%;
    }

    .box h2[data-v-f4211ad8] {
        margin: 0;
        font-size: 1em;
    }
}

@media (max-width: 480px) {
    .round {
        top: 72%;
    }

    .round1 {
        top: 84%;
    }


}


.profile {
    background-color: white;
    height: 9vh;
    border-radius: 70%;
}

.profile-text {
    font-size: 1rem;
    font-family: 'Trebuchet MS', Arial, sans-serif;
}

.profile-box {
    height: 19vh;
    width: 26vh;
    padding: 1.5em;
}

.img {
    height: 16vh;
    width: 8vw;
}

.img1 {
    height: 16vh;
    width: 8vw;
}

@media (max-width: 1321px) {
    .box {
        flex: 0 0 45%;
        max-width: 25%;
    }

    .profile-box {
        height: 21vh;
        width: 29vh;
    }
}

@media (max-width: 1000px) {
    .box h2[data-v-f4211ad8] {
        margin: 0;
        font-size: 1.4em;
    }
}

@media (max-width: 768px) {
    .box {
        flex: 0 0 48%;
        max-width: 32%;
    }

    .box h2[data-v-f4211ad8][data-v-f4211ad8] {
        margin: 0;
        font-size: 1.2em;
    }

    .heading {
        font-size: 2rem;
    }

    .logo {
        width: 30vw;
    }

    .container {
        padding: 5em 1em;
    }

    .profile-box {
        height: 21vh;
        width: 33vh;
    }
}

@media (max-width: 490px) {
    .container {
        gap: 0;
    }

    .box {
        flex: 0 0 48%;
        max-width: 48%;
        margin: 5px;
    }

    .logo {
        width: 80px;
    }

    .heading {
        font-size: 1rem;
    }

    .profile {
        height: 6vh;
    }

    .heading[data-v-f4211ad8] {
        font-size: 1rem;
    }

    .box h2[data-v-f4211ad8][data-v-f4211ad8][data-v-f4211ad8] {
        margin: 0;
        font-size: 1em;
    }

    .box img[data-v-f4211ad8] {
        max-width: 100vw;
        height: auto;
        display: block;
        margin: 0 auto 1em;
    }
}

@media (max-width: 400px) {
    .box h2[data-v-f4211ad8][data-v-f4211ad8][data-v-f4211ad8] {
        margin: 0;
        font-size: 11px
    }
}

@media (max-width: 572px) {
    .logo {
        width: 26vw;
    }

    .container {
        padding: 10em 0em;
    }

    .box {
        flex: 0 0 48%;
        max-width: 26%;
    }

    .profile-text[data-v-f4211ad8] {
        font-size: 0.5em;
        font-family: 'Trebuchet MS', Arial, sans-serif;
    }

    .img1[data-v-f4211ad8] {
        height: 11vh;
        width: 13vw;
    }
}

@media (max-width: 636px) {
    .profile-box {
        height: 18vh;
    }

    .heading[data-v-f4211ad8] {
        font-size: 1rem;
    }

    .profile-text[data-v-f4211ad8] {
        font-size: 0.6rem;
        font-family: 'Trebuchet MS', Arial, sans-serif;
    }
}
</style>
