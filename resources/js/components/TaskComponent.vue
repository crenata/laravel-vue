<template>
    <div class="container">
        <div class="modal fade" id="modal-form" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Modal Form</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <div class="form-group">
                            <label for="">Task Title</label>
                            <input v-model="task.title" type="text" name="title" id="" class="form-control">
                        </div>
                        <div class="form-group">
                            <label for="">Priority</label>
                            <select v-model="task.prior" name="prior" class="form-control">
                                <option value="low">Low</option>
                                <option value="medium">Medium</option>
                                <option value="high">High</option>
                            </select>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save changes</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">
                        <div class="row">
                            <div class="col-6">
                                <p class="m-0">Task List</p>
                            </div>
                            <div class="col-6 text-right">
                                <button class="btn btn-primary btn-sm" @click="showModal()">+ Add Task</button>
                            </div>
                        </div>
                    </div>

                    <div class="card-body">
                        <table class="table table-bordered table-striped">
                            <thead>
                                <tr>
                                    <th>#</th>
                                    <th>Task Title</th>
                                    <th>Level</th>
                                    <th></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(task, index) in tasks" :key="index">
                                    <td>{{ index + 1 }}</td>
                                    <td>{{ task.title }}</td>
                                    <td>{{ task.prior }}</td>
                                    <td>
                                        <button class="btn btn-default btn-sm">Edit</button>
                                        <button class="btn btn-danger btn-sm">Delete</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "TaskComponent",
        data() {
            return {
                tasks: [],
                task: {
                    title: '',
                    prior: ''
                }
            };
        },
        methods: {
            showModal() {
                $('#modal-form').modal('show');
            },
            getTasks() {
                axios.get('task').then(response => {
                    this.tasks = response.data.data;
                    console.log(this.tasks);
                });
            }
        },
        mounted() {
            this.getTasks();
        }
    }
</script>

<style scoped>

</style>
