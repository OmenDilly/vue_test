<template>
    <div class='timer__card'>
        <span>{{timer.value}}</span>
        <div class='card__actions'>
            <span classs='play'>
                <svg xmlns="http://www.w3.org/2000/svg" fill='white' viewBox="0 0 18 18" width="18px" height="18px">
                    <path d="M0 0h24v24H0z" fill="none"/>
                    <path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/>
                </svg>
            </span>
            <span class='stop'>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 18 18" fill="white" width="18px" height="18px">
                    <path d="M0 0h24v24H0z" fill="none"/>
                    <path d="M6 6h12v12H6z"/>
                </svg>
            </span>
        </div>
    </div>
</template>