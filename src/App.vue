<script>
    let id = 0;

    export default {
        created() {
            window.addEventListener('keydown', event => {
                const key = event.key;

                for(const data of this.keyData)
                {
                    if(data.key === key)
                    {
                        const div = document.querySelector(`div[data-key='${key}']`);
                        div.classList.add('active');
                        const audio = document.querySelector(`audio[data-key='${key}']`);
                        audio.currentTime = 0;
                        audio.play();
                        break;
                    }
                }
            });
        },
        data() {
            return {
                keyData: [
                    { id: id++, key:'a', sound:'clap' },  
                    { id: id++, key:'s', sound:'hihat' },
                    { id: id++, key:'d', sound:'kick' },
                    { id: id++, key:'f', sound:'openhat' },
                    { id: id++, key:'g', sound:'boom' },
                    { id: id++, key:'h', sound:'ride' },
                    { id: id++, key:'j', sound:'snare' },
                    { id: id++, key:'k', sound:'tom' },
                    { id: id++, key:'l', sound:'tink'}
                ]
            };
        },
        methods: {
            removeActive(event) {
                event.target.classList.remove('active');
            }
        }
    };
</script>

<template>
    <div class="container">
        <div class="box" v-for="data of keyData" :key="data.id" :data-key="data.key" @transitionend="removeActive">
            <kbd class="key">{{data.key}}</kbd>
            <p class="sound">{{data.sound}}</p>
        </div>
    </div>

    <audio data-key="a">
        <source src="./assets/audio/Clap.wav">
    </audio>
    <audio data-key="s">
        <source src="./assets/audio/Hihat.wav">
    </audio>
    <audio data-key="d">
        <source src="./assets/audio/Kick.wav">
    </audio>
    <audio data-key="f">
        <source src="./assets/audio/Openhat.wav">
    </audio>
    <audio data-key="g">
        <source src="./assets/audio/Boom.wav">
    </audio>
    <audio data-key="h">
        <source src="./assets/audio/Ride.wav">
    </audio>
    <audio data-key="j">
        <source src="./assets/audio/Snare.wav">
    </audio>
    <audio data-key="k">
        <source src="./assets/audio/Tom.wav">
    </audio>
    <audio data-key="l">
        <source src="./assets/audio/Tink.wav">
    </audio>
</template>

<style scoped>
    .container {
        display: grid;
        grid-template-columns: repeat(9, 1fr);
        gap: 30px;
    }

    .box {
        width: 90px;
        height: 90px;
        border: 3px solid black;
        border-radius: 10px;
        background-color: hsla(0, 0%, 50%, .2);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transition: all 100ms ease;
    }

    .active {
        border: 3px solid hsl(49, 100%, 50%);
        scale: 1.1;
    }

    p,
    kbd {
        user-select: none;
    }

    .key {
        color: white;
        font-size: 2rem;
        text-transform: uppercase;
    }

    .sound {
        color: hsl(49, 100%, 50%);
        font-size: .9rem;
        text-transform: uppercase;
    }
</style>