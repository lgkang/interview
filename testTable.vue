<template>
    <div>
        <el-data-table v-bind="tableConfig" @header-click="headerClick">
            <template slot="three" slot-scope="{scope}">
                <span class="red">{{scope.row}}</span>
            </template>
        </el-data-table>
    </div>
</template>

<script>
    export default {
        name: "dataTable",
        data() {
            return {
                tableConfig: {
                    url: "/example/users",
                    requests: {
                        axios: this.$axios, //配置你的axios
                        getData: {
                            method: "get",
                            url: "http://www.baidu.com",
                            errorHandler: this.errorHandler,
                        }
                    },
                    columns: [
                        {
                            prop: "name",
                            label: "用户名"
                        },
                        {
                            prop: "age",
                            label: "年龄"
                        },
                        {
                            prop: "count",
                            label: "成绩",
                            slots: "three" //配置slots
                        }
                    ],
                    searchForm: [
                        {
                            type: "input",
                            id: "name",
                            label: "用户名",
                            el: {
                                placeholder: "请输入"
                            }
                        }
                    ],
                    form: [
                        {
                            type: "input",
                            id: "name",
                            label: "用户名",
                            el: {
                                placeholder: "请输入"
                            },
                            rules: [
                                {
                                    required: true,
                                    message: "请输入用户名",
                                    trigger: "blur"
                                }
                            ]
                        }
                    ]
                }
            };
        },
        methods: {
            errorHandler(err, callback) {
                //处理数据
                err = {data: 2};
                callback(err);
            },
            headerClick(column, event) {
                console.log(column);
            },
            getTable() {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        resolve({data: 1});
                    }, 2000);
                });
            }
        }
    };
</script>

<style scoped>
    .red {
        color: red
    }
</style>
