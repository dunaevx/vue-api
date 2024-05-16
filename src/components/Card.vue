<script>
export default {
    props: ['card']
};
</script>

<template>
    <article class="card">
        <div class="card__img">
            <img :src="card.image" :alt="card.name" />
        </div>
        <div class="card__content">
            <div class="section">
                <h2>{{ card.name }}</h2>
                <h4>{{ card.status + " - " + card.species}}</h4>
            </div>
            <div class="section">
                <span>Last known location:</span>
                <p>{{ card.location.name }}</p>
            </div>
            <div class="section">
                <span>First seen in:</span>
                <p>{{ card.origin.name }}</p>
            </div>
        </div>
    </article>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.card{
    width: 600px;
    height: 220px;
    display: flex;
    overflow: hidden;
    background: rgb(60, 62, 68);
    border-radius: 0.5rem;
    margin: 0.75rem;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
    
    font-family: 'Roboto', sans-serif;
}

h2{
    font-size: 20px;
}

h2:hover{
    color: #ffa500;
}

p:hover{
    color: #ffa500;
}

span{
    color: #9e9e9e;
}

/* img */

img{
    width: 100%;
    height: 100%;
    margin: 0px;
    opacity: 1;
    transition: opacity 0.5s ease 0s;
    object-position: center center;
    object-fit: cover;
}

/* card__content */
.card__content{
    position: relative;
    padding: 0.75rem;
    color: rgb(255, 255, 255);
    display: flex;
    flex-direction: column;
}

.section{
    flex: 1 1 0%;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

</style>
