<template>

    <div>
        <div class="container">
            <ul class="nav">
                <li class="nav-item">
                    <a class="nav-link " @click.prevent="newTab(components.patient) " href="#">Patients</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="newTab(components.doctor)"  href="#">Doctors</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="newTab(components.visitor)" href="#">Visitors</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="newTab(components.billing)" href="#">Billing</a>
                </li>
            </ul>
        </div>
        <b-card no-body>
            <b-tabs small card v-model="tabIndex">
                <!-- Render Tabs -->
                <b-tab   v-for="i in tabs" :key="i">
                    <template slot="title">
                        {{currentComponent[i]}} <a href="#" @click="()=>closeTab(i, currentComponent[i] )" ><i class="fa fa-close ml-1"></i> </a>
                    </template>

                    <keep-alive>
                        <component :is="currentComponent[i]"

                        ></component>
                    </keep-alive>


                    <!--Tab Contents {{i}}-->

                    <!--<b-btn size="sm" variant="danger" class="float-right" @click="()=>closeTab(i)">-->
                        <!--Close tab-->
                    <!--</b-btn>-->
                </b-tab>

                    <!-- New Tab Button (Using tabs slot) -->
                    <!--<b-nav-item  v-if="moreTabs" slot="tabs" @click.prevent="newTab(components.default)" href="#">-->
                        <!--+-->
                    <!--</b-nav-item>-->


                <!-- Render this if no tabs -->
                <div slot="empty" class="text-center text-muted">
                    There are no open tabs
                    <br> Open a new tab using + button.
                </div>
            </b-tabs>
        </b-card>

    </div>

</template>

<script>
    import { Tabs } from 'bootstrap-vue/es/components';
    Vue.use(Tabs);

    export default {
        name: "tab",
        props : [],
        data : function () {
            return{
                tabs: [],
                tabCounter: 0,
                moreTabs : true,
                tabIndex: 1,
                components : {
                    doctor : 'doctor',
                    patient : 'patient',
                    visitor : 'visitor',
                    billing : 'billing',
                    default : 'default',
                },
                currentComponent : [],
            }
        },
        methods : {
            closeTab (x, component) {
                for (let i = 0; i < this.tabs.length; i++) {
                    if (this.tabs[i] === x) {
                        this.tabs.splice(i, 1)
                        this.currentComponent[x] = this.components.default
                    }
                }

                // for (let i = 0; i < this.currentComponent.length; i++) {
                //     if(this.currentComponent[i] === component){
                //         this.currentComponent.splice(i, 1)
                //     }
                //
                //
                // }



                this.moreTabs = true
            },
            newTab (component) {

                var exist = false;
                for (let i = 0; i < this.currentComponent.length; i++) {
                    if(this.currentComponent[i] === component){
                        exist = true
                    }
                }

                if (!exist){
                    if(this.tabs.length <= 5){
                        this.tabs.push(this.tabCounter++)
                    }
                    this.currentComponent.push(component)

                }

                if(this.tabs.length === 5){
                    this.moreTabs = false
                }else {
                    this.moreTabs = true
                }
                this.tabIndex = 1


            },
        },
        created : function(){
            this.newTab(this.components.doctor)
        },
        // watch : {
        //     tabCounter : function (val, oldVal) {
        //         this.timer =
        //
        //     },
        // }

    }
</script>


<style scoped>

</style>