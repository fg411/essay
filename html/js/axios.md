# Axios的使用与封装

## 为什么用`axios`
项目开发中，向服务器请求是必不可少的，在Vue项目的开发中，`axios`库是很常见的一个库。常见的`axios`的特性有 拦截请求和响应、取消请求、转换json、客户端防御XSRF等

## 安装

`npm` 安装 `axios`，如果可以的话，再安装一个`qs`库
```shell
> npm install axios
> npm install qs // 用来序列化post类型的数据
```

## 引用

既然要封装，那项目应该会有一个文件夹用来存储公用的类或者文件。按照个人习惯，我在 `src` 文件夹下新建 `lib` 文件夹 并新建 `http.js`
```javascript
import axios from 'axios'; // 引入axios
import QS from 'qs'; // 引入qs模块
```

### 设置请求超时
通过axios.defaults.timeout设置默认的请求超时时间。
```javascript
axios.defaults.timeout = 5000;
```
### 拦截器

请求拦截器的使用
```javascript
// 例如：在Http请求的header中添加 token
axios.interceptors.request.use(
    config => {
        // 解析token
        const access_token = 123; // 本地保存(cookie/local Storage/session 等)的`token`或者`vuex`中保存的`token`
        config.headers.Authorization = access_token;
        return config;
    },
    err => {
        return Promise.reject(err);
    }
)
```
响应拦截器
```javascript
// 例如：在请求响应后判断是正常响应，不正常时提示。
// 如果服务端对返回体进行包装的话，可在这里进行处理。
axios.interceptors.response.use(
	response => {
		if (response.status === 200) {
            return Promise.resolve(response);
        } else {
            return Promise.reject(response);
        }
	},error => {
		if (error.response.status) {
			switch (error.response.status) {
				case 404:
					// code: 提示 404 错误
					break;
				case 500:
					// code: 提示 500  或其他错误
					break;
			}
			return Promise.reject(error.response);
		}
	}
)
```

### 封装get方法 和 post 方法
http请求常用的方法有 get、post、put、delete，下面对 get、post 进行了简单的封装

```javascript
// get 方法
export function get(url, params) {
	return new Promise((resolve, reject) => {
		axios.get(url, {params}).then(res => {
			resolve(res.data)
		}).catch(error => {
			reject(error.data)
		})
	})
}
// post 方法
export function post(url, params) {
	return new Promise((resolve, reject) => {
		axios.post(url, QS.stringify(params)).then(res => {
			resolve(res.data)
		}).catch(error => {
			reject(error.data)
		})
	})
}
```
