<template>
	<div>
		{{content}}
		<hr/>
		{{totalElements}}
	</div>
</template>

<script>
    export default {
        data() {
            return {
                content: '',
                totalElements: ''
            }
        },
        created() {
            const _this = this;
            axios.get("findAllUsers/1/6").then(function (response) {
                console.log(response);
                _this.content = response.data.content;
                _this.totalElements = response.data.totalElements;
            }).catch(function (error) {
                console.log(error);
            }).finally(function () {
                console.log('最终');
            });
            /*axios.post("http://112.124.19.70:8081/users/saveUsers/", {
                    content: {
                        id: null,
                        username: "哈哈啊哈哈哈",
                        password: "哈哈啊哈哈哈"
                    },
                    //设置
                    headers: {
                        'content-type': 'application/x-www-form-urlencoded'
                    }
                }
            ).then(function (response) {
                console.log(response);
            })*/

            // 将两个请求一起发送，只要有一个失败，就算失败，必须都请求成功
            // 获取省市数据的需求
            this.$axios.all([
                axios.post(""),
                axios.get("http://112.124.19.70:8081/findAllUsers/1/6")
            ])
                // 分发响应
                .then(this.$axios.spread())
                .catch(function (error) {
                    console.log(error);
                })
        }
    }
</script>