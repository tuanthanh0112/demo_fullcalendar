<template>
    <div>
        <Fullcalendar 
            :options="calendarPlugins"
            :select="handleSelect"
            
        /> 
    </div>
</template>
<script>

import Fullcalendar from "@fullcalendar/vue";
import DayGridPlugin from "@fullcalendar/daygrid";
import TimeGridPlugin from "@fullcalendar/timegrid";
import InteractionPlugin from "@fullcalendar/interaction";
import ListPlugin from "@fullcalendar/list";
import { mapGetters } from "vuex";
export default {
    name: "CalenDar",
    components: {
        Fullcalendar
    },
    data() {
        return {
            calendarPlugins: {
                plugins : [
                DayGridPlugin,
                TimeGridPlugin,
                InteractionPlugin,
                ListPlugin
                ],
                headerToolbar: { right: 'dayGridMonth,timeGridWeek,timeGridDay', center: 'title',left:'prev,next today', },
                selectable: true,
                weekends: false,
                events: "EVENTS",
            },
            computed: {
                ...mapGetters(["EVENTS"])
            },
            methods: {
                handleSelect(arg){
                    console.log(arg)
                }
            },
        }
    }
}
</script>
<style lang="">
    
</style>