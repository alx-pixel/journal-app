<template>
    <div class="entry-container mb-3 pointer p-2" 
    @click="$router.push({ name: 'entry', params: { id: entry.id }})">
        <div class="entry-title d-flex">
            <span class="text-success fs-5 fw-bold">{{ day }}</span>
            <span>{{ month }}</span>
            <span>{{ yearDay }}</span>
        </div>

        <div class="entry-description">
            {{ shortText }}
        </div>
    </div>
</template>

<script>

const months = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio','Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']
const days   = ['Domingo','Lunes','Martes','Miércoles','Jueves','Viernes','Sábado']

export default {
    props: {
        entry: {
            type: Object,
            required: true
        }
    },
    computed: {
        shortText() {
            return ( this.entry.text.length > 130 )
            ? this.entry.text.substring(0, 130) + '...'
            : this.entry.text
        },
        day() {
            const date = new Date( this.entry.date )
            console.log( date )
            return date.getDate()
        },
        month() {
            const date = new Date( this.entry.date )
            return months[ date.getMonth() ]

        },
        yearDay() {
             const date = new Date( this.entry.date )
             return `${ date.getFullYear() }, ${ days[ date.getDay() ]}`
        }
    }
}
</script>

<style lang="scss" scoped>
    .entry-container{
        transition: 0.2 all ease-in;

        &:hover {
            background-color: lighten($color: grey, $amount: 45);
            transition: 0.2 all ease-in;
        }

        .entry-description{
            font-size: 1rem;
        }
    }

    
</style>