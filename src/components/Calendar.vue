<template>
    <div class='demo-app'>
    <div class='demo-app-main'>
       <Fullcalendar 
            class='demo-app-calendar'
            :options="calendarPlugins"
        > 
      </FullCalendar>
    </div>
  </div>
</template>
<script>
import Fullcalendar from "@fullcalendar/vue";
import DayGridPlugin from "@fullcalendar/daygrid";
import TimeGridPlugin from "@fullcalendar/timegrid";
import InteractionPlugin from "@fullcalendar/interaction";
import ListPlugin from "@fullcalendar/list";
import resourceTimelineDayPlugin from "@fullcalendar/resource-timeline";
import { createEventId } from "../event/event-utils";
import { mapActions } from "vuex";
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
                ListPlugin,
                resourceTimelineDayPlugin
                ],
                headerToolbar: { 
                    right: 'dayGridMonth,timeGridWeek,timeGridDay', 
                    center: 'title',  
                    left:'prev,next today', 
                },
                // initialEvents: INITIAL_EVENTS,
                selectable: true,

                dayMaxEvents: true,
                weekends: false,
                selectMirror: true,
                select: this.handleDateSelect,
                eventClick: this.handleEventClick,
                eventsSet: this.handleEvents,
                editable: true,
                droppable: true 
            },
            currentEvents:[]
        }
    },
    methods: {
        ...mapActions([
            'updateEvent'
        ]),
        handleWeekendsToggle() {
             this.calendarPlugins.weekends = !this.calendarPlugins.weekends // update a property
         },

        handleDateSelect(selectInfo) {
            let title = prompt('Please enter a new title for your event')
            let calendarApi = selectInfo.view.calendar
            calendarApi.unselect() // clear date selection
            if (title) {
                    calendarApi.addEvent({
                    id: createEventId(),
                    title,
                    start: selectInfo.start,
                    end: selectInfo.end,
                    allDay: selectInfo.allDay
                })
            }
        },
        handleEventClick(clickInfo) {
            if(confirm(`'xoa di dung ngai' '${clickInfo.event.title}'`)){
                clickInfo.event.remove()
            }
        },
        handleEvents(events) {
            this.currentEvents = events
        },
        onEventDrop({event}){
            return this.updateEvent(event)
        }
    }
}
</script>
<style lang="">
    
</style>