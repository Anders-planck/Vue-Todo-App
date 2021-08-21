<template>
  <div class="menu">
      <h1>Manager your Time with my <span>TODO-App</span></h1>
  </div>
  <div class="todo">
      <div class="todoWork">
          <div class="insertTodo">
            <div>
                <form class="todoInput" @submit.prevent="addTodo">
                    <input type="text" v-model="newTodo.content"/>
                    <button type="submit">Add Todo</button>
                </form>
            </div>
            <transition name="preview">
                <div class="preview" v-if="content">
                    <h2>Preview</h2>
                    <ul>
                        <li><span>content:</span><p class="value"> {{newTodo.content}}</p></li>
                        <li><span>status:</span><p class="value">{{newTodo.done}}</p></li>
                    </ul>
                </div>
            </transition>
        </div>

        <div class="todoLists">
            <h2>Events TO DO...</h2>
            <ul>
                <li @click="markTodo(todo)" v-for="todo in Todos" :key="todo.time" :class="{do : todo.done}">
                    <div class="info">
                        <p>{{todo.content}}</p>
                        <h5>{{todo.time}}</h5>
                    </div>
                    <span class="status done" v-if="todo.done" >Done</span>
                    <span v-else class="status doIt">To Do</span>
                    <span class="remove" @click="removeTodo(todo.id)">Delete</span>
                </li>
            </ul>
            <div class="niente" v-if="Todos.length==0">
                <h3>NO EVENT</h3>
            </div>
        </div>
      </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
    name:'Todo',
    data(){
        return{
            newTodo:null,
            Todos: [],
        }
    },
    created(){
        this.newTodo=this.inizialise()
    },
    computed:{
        content(){
            if(this.newTodo.content !=null && this.newTodo.content.length>=5 )
                return true 
            return false
        }
    },
    components:{},
    methods:{

        now(){
            return moment().format("dddd Do MMMM YYYY - h:mm:ss a")
        },
        addTodo(){
            this.newTodo.id=this.now()
            this.newTodo.time=this.now()
            this.Todos.push(this.newTodo)
            this.newTodo=this.inizialise()
        },
        inizialise(){

            let newTodo={
                content: null,
                done: false,
                time: null,
                id: null
            }
            return newTodo
        },
        markTodo(todo){
            todo.done=!todo.done;
        },
        removeTodo(id){
            this.Todos=this.Todos.filter(todo =>{
                return todo.id !=id
            })
        }
    }
}
</script>

<style scope lang='scss'>
    .menu{
        width: 100%;
        margin: 6rem 0 0  0;
        text-align: center;
        h1{
            span{
                font-weight: 900;
                color: #42b983;
            }
        }
    }


    .todo{
        padding: 1rem;
        position: relative;
        .todoWork{
            width: 450px;
            margin: 0 auto;
            max-width: 450px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 1rem;
            .insertTodo{
                width: 100%;
                display: flex;
                flex-direction: column;
                text-align: center;
                .todoInput{
                    display: flex;
                    width: 100%;
                    margin-bottom: 3rem;
                    margin-top:6rem ;
                    input{
                        width: 100%;
                        height: 30px;
                        outline: none;
                        border: none;
                        font-size: 1.5rem;
                        font-style: italic;
                        background: rgba(22, 22, 22, 0.048);
                        border-radius: 2px;
                        padding: 1rem;
                    }
                    button{
                        width: 100px;
                        background: #42b983;
                        outline: none;
                        border-radius: 2px;
                        border: none;
                        color: white;
                        cursor: pointer;
                    }
                }
                .preview{
                    text-align: left;
                    h2{
                        margin: 1rem 0;
                        display: block;
                        text-align: center;
                    }
                    ul>li{
                        margin: 1rem 0;
                    }
                    ul>li>span{
                        font-weight: 900;

                    }
                    ul>li>p{
                        padding: 0.5rem;
                        overflow-wrap: break-word;
                        width: 450px;
                        display: block;
                        color: #32c482;
                        line-height: 1.1rem;
                        font-weight: bold;
                    }
                }
            }
            .todoLists{

                margin: 3rem 0;
                min-width: 450px;
                h2{
                    display: block;
                    text-align: center;
                }
                ul{
                    list-style: none;
                    margin: 2rem 0;
                    .do{
                        color: white;
                        background-color:#42b98396;
                        font-weight: 900;
                        font-style: italic;
                    }
                    li{
                        width: 450px;
                        padding: 1rem 0.5rem 1rem 1rem;
                        margin: 1rem 0;
                        border-radius: 5px;
                        background:rgba(0, 0, 0, 0.027);
                        box-shadow: 10px 9px 26px 5px rgba(237,237,237,0.56);
                        .status{
                            display: block;
                            text-align: right;
                            padding-right:1rem;
                            margin: 1rem 1rem 0rem 0rem;
                            font-weight: 900;
                            text-transform: capitalize;
                        }

                        .done{
                            color: #03532f;
                        }

                        .doIt{
                            color: rgba(255, 0, 0, 0.801);
                        }

                        .remove{
                            font-size: 0.85rem;
                            font-weight: 900;
                            color: white;
                            background: rgba(243, 140, 140, 0.9);
                            padding: 0.5rem 1rem;
                            border-radius:5px ;
                            cursor: pointer;
                        }

                        .info{
                            display: flex;
                            flex-direction: column;
                            p{
                                font-weight: 900;
                                margin-bottom: 0.5rem;
                                overflow-wrap: break-word;
                                line-height: 1.1rem;
                            }
                        }
                    }

                }

                .niente{
                    text-align: center;
                    color: #42b983;
                }
            }
        }
    }

    .preview-enter-active,
    .preview-leave-active{
        transition: all 1s ease-in-out;
    }

    .preview-enter{
        transform: translateY(-250px);
        opacity: 0;
    }
    .preview-enter-to{
        transform: translateY(0);
        opacity: 1;
    }
    .preview-leave-to{
        transform: translateY(-250px);
        opacity: 0;
    }
    .preview-leave{
        transform: translateY(0);
        opacity: 1;
    }

</style>