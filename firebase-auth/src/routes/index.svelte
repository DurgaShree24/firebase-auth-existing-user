<script lang="ts">

    // Import the functions you need from the SDKs you need
    import { initializeApp } from "firebase/app";
    import { getAuth, signInWithEmailAndPassword,signOut, type User, onAuthStateChanged } from "firebase/auth";
    import { onMount } from 'svelte';

    let email = "";
    let password = "";
    let user: User | null ;

    // Your web app's Firebase configuration
    const firebaseConfig = {
    apiKey: "AIzaSyAGKieWupJ7cs8gVptGfFKrAjjUDKk1r7Y",
    authDomain: "fir-auth-69fcb.firebaseapp.com",
    projectId: "fir-auth-69fcb",
    storageBucket: "fir-auth-69fcb.appspot.com",
    messagingSenderId: "1070824312133",
    appId: "1:1070824312133:web:1d2205ca043122f79d822c"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    // Initialize Firebase Authentication and get a reference to the service
    const auth = getAuth(app);

    const login = () => {
        // Initialize Firebase Authentication and get a reference to the service
        const auth = getAuth(app);

        signInWithEmailAndPassword(auth, email, password)
        .catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            console.log(errorCode, errorMessage)
        });

    };
    const logout = async () => {
        const auth = getAuth(app);
        signOut(auth);
        email = "";
        password = "";
    };

    onMount (async () => {
        const auth = getAuth(app);
        onAuthStateChanged(auth, (newUser) => {
            user = newUser;
        });
    })

</script>

<div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm ">
    <form>
      <div class="form-group mb-6">
{#if user}
    <p>Signed In</p>
    <button on:click={logout} class="
    px-6
    py-2.5
    bg-blue-600
    text-white
    font-medium
    text-xs
    leading-tight
    uppercase
    rounded
    shadow-md
    hover:bg-blue-700 hover:shadow-lg
    focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
    active:bg-blue-800 active:shadow-lg
    transition
    duration-150
    ease-in-out">Logout</button>
    {:else}
    <input type="email" id="email" placeholder="Enter email ID" bind:value={email} class="
      px-6
      py-2.5
      m-2
      text-white
      font-medium
      text-xs
      leading-tight
      uppercase
      rounded
      shadow-md
      hover:bg-blue-100 hover:shadow-lg
      focus:bg-blue-100 focus:shadow-lg focus:outline-none focus:ring-0
      active:bg-blue-200 active:shadow-lg
      transition
      duration-150
      ease-in-out">
    <input type="password" id="password" placeholder="Enter password" bind:value={password} class="
    px-6
    py-2.5
    m-2
    text-white
    font-medium
    text-xs
    leading-tight
    uppercase
    rounded
    shadow-md
    hover:bg-blue-100 hover:shadow-lg
    focus:bg-blue-100 focus:shadow-lg focus:outline-none focus:ring-0
    active:bg-blue-200 active:shadow-lg
    transition
    duration-150
    ease-in-out">
    <button on:click={login} class="
    px-6
    py-2.5
    m-5
    bg-blue-600
    text-white
    font-medium
    text-xs
    leading-tight
    uppercase
    rounded
    shadow-md
    hover:bg-blue-700 hover:shadow-lg
    focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
    active:bg-blue-800 active:shadow-lg
    transition
    duration-150
    ease-in-out">Login</button>
{/if}
</div>
</form>
</div>