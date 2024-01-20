<template>
    <layout-div>
        <div class="row justify-content-md-center">
          
                <nav class="navbar navbar-expand-lg navbar-light NavabarStyle">
                    <div class="container-fluid">
                        <!-- <ul class="navbar-nav addbutton">
                            <li class="nav-item">
                                <a @click="logoutAction()" class="nav-link " style="text-align: center; font-size: 22px; color:  #FFFFFF;" aria-current="page"
                                        href="#">+</a>
                             
                            </li>
                        </ul> -->
                        <ul class="navbar-nav">
                            <li style="color: #FFFFFF; font-weight: 700;" class="nav-item">
                              User Name
                            </li>
                        </ul>
                        <div class="d-flex">
                            <ul class="navbar-nav">
                                <li class="nav-item">
                                    <a @click="logoutAction()" class="nav-link " style="color: #FFFFFF;" aria-current="page"
                                        href="#">Logout</a>
                                </li>
                            </ul>

                        </div>
                    </div>
                </nav>



                <div class="col-12 mt-4">
                    <nav class="navbar navbar-expand-lg navbar-light listStyle">
                        
                        <div class="column is-12" style="display: contents;">

                         
                            <input class="form-control" name="name" v-model="name" style=" border-top-right-radius: 0px;
                               border-bottom-right-radius: 0px; height: 80px;" type="text" placeholder="Add Today Task">
                          
                            <button class="btn"
                                style=" border-top-left-radius: 0px;
                               border-bottom-left-radius: 0px; height: 80px; width:134px; background-color: #9395D3; color: white; font-weight: 700;"
                                type="submit">Add Task</button>
                            
                        </div>
                    </nav>
                </div>


                <div class="col-12 mt-4">

                    <nav class="navbar navbar-expand-lg navbar-dark listStyle">
                        <div class="container-fluid">
                            <div>
                                <div>
                                    <a class="navbar-brand" style="color: #9395D3; font-size: 15px; font-weight: 700;"
                                        href="#">TODO TITLE</a>

                                </div>
                                <div>
                                    <a class="navbar-brand" style="color: black;  font-size: 11px; font-weight: 700;"
                                        href="#">TODO SUB TITLE</a>

                                </div>
                            </div>
                            <div class="collapse navbar-collapse" id="mynavbar">
                                <ul class="navbar-nav me-auto">
                                    <li class="nav-item">

                                    </li>
                                    <li class="nav-item">

                                    </li>
                                    <li class="nav-item">
                                        <!-- <a class="nav-link" href="javascript:void(0)" style="color: black;">Edit</a> -->
                                    </li>

                                </ul>
                                <div class=" d-flex">
                                    <ul class="navbar-nav me-auto">
                                        <li class="nav-item">
                                            <Modal />
                                         
                                        </li>
                                        <li class="nav-item">
                                            <!-- <a class="nav-link" href="javascript:void(0)" style="color: #9395D3;"> <font-awesome-icon icon="trash" /></a> -->
                                        </li>
                                        <li class="nav-item">
                                            <a class="nav-link" href="javascript:void(0)" style="color: #9395D3;">
                                                <font-awesome-icon icon="trash" /></a>
                                        </li>
                                        <li class="nav-item">
                                            <!-- <a class="nav-link" href="javascript:void(0)" style="color: #9395D3;"> <font-awesome-icon icon="trash" /></a> -->
                                        </li>
                                        <li class="nav-item">
                                            <a class="nav-link" href="javascript:void(0)" style="color: #9395D3;">
                                                <font-awesome-icon icon="check" /></a>
                                        </li>
                                    </ul>
                                </div>

                            </div>
                        </div>
                    </nav>
                </div>
                <div class="col-12 mt-4">




                    <nav class="navbar navbar-expand-lg navbar-light listStyle">
                        <div class="container-fluid">
                            <a class="navbar-brand" style="color: #FFFFFF;" href="#">Dashboard</a>
                            <div class="d-flex">
                                <ul class="navbar-nav">
                                    <li class="nav-item">
                                        <a @click="logoutAction()" class="nav-link " style="color: #FFFFFF;"
                                            aria-current="page" href="#">Logout</a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </nav>
                </div>
                <div class="col-12 mt-4">


                    <nav class="navbar navbar-expand-lg navbar-light listStyle">
                        <div class="container-fluid">
                            <a class="navbar-brand" style="color: #FFFFFF;" href="#">Dashboard</a>
                            <div class="d-flex">
                                <ul class="navbar-nav">
                                    <li class="nav-item">
                                        <a @click="logoutAction()" class="nav-link " style="color: #FFFFFF;"
                                            aria-current="page" href="#">Logout</a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </nav>
                </div>
        


        </div>
    </layout-div>
</template>
  
<script>
import axios from 'axios';
import LayoutDiv from '../LayoutDiv.vue';
import Modal from '../pages/ViewUpdateModelPage.vue'



export default {
    name: 'DashboardPage',
    components: {
        LayoutDiv,
        Modal
    },
    data() {
        return {
            user: {},
        };
    },
    created() {
        this.getUser();
        if (localStorage.getItem('token') == "" || localStorage.getItem('token') == null) {
            this.$router.push('/')
        } else {
            this.getUser();
        }

    },
    methods: {
        getUser() {
            axios.get('/api/user', { headers: { Authorization: 'Bearer ' + localStorage.getItem('token') } })
                .then((r) => {
                    this.user = r.data;
                    return r
                })
                .catch((e) => {
                    return e
                });
        },

        logoutAction() {
            axios.post('/api/logout', {}, { headers: { Authorization: 'Bearer ' + localStorage.getItem('token') } })
                .then((r) => {
                    localStorage.setItem('token', "")
                    this.$router.push('/')
                    return r
                })
                .catch((e) => {
                    return e
                });
        }

    },
};
</script>

<style>
.NavabarStyle {
    background-color: #9395D3;
    height: 80px;
}

.listStyle {
    background-color: #ffff;
    height: 80px;
    border-radius: 10px;
    box-shadow: rgba(17, 17, 26, 0.1) 0px 4px 16px, rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 56px;
}
.listStyle1 {
    background-color: #ffff;
    height: 80px;
    border-radius: 10px;
    box-shadow: rgba(17, 17, 26, 0.1) 0px 4px 16px, rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 56px;
}
.AddButtonStyle {
    background-color: #c7c8ed;
    height: 80px;
}

.addbutton {
    display: flex;
    justify-content: center;
    background: #9395D3;
    width: 52px;
    height: 52px;
    border-radius: 50%;
    box-shadow: rgba(17, 17, 26, 0.1) 0px 4px 16px, rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 56px;

}

.containerStyle {
    background-color: #c7c8ed;
    height: 100vh;
}
</style>

<playground-resources lang="json">
{
    "css": [
        "https://use.fontawesome.com/releases/v5.1.0/css/all.css"
    ]
}
</playground-resources>