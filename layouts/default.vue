<template>
    <header>
        <nav class="flex w-auto bg-blue-600 mx-1 justify-between shadow-2xl rounded-md">
            <h1 class=" text-5xl my-auto" >ecom</h1>
            <ul class="flex list-none">
                <li class="mx-1 md:mx-4 my-auto">home</li>
                <li class="mx-1 md:mx-4 my-auto">product</li>
                <li class="mx-1 md:mx-4 my-auto">about</li>
            </ul>
        </nav>
    </header>
    <div>
        <slot></slot>
    </div>
    <footer></footer>
</template>