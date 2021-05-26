### Axios.interceptors를 활용해 JWT 토큰 갱신
``` js
instance.interceptors.response.use(
        response => { // 서버에 요청을 보내고 나서 응답을 받기 전에 어떤 처리를 할 수 있다.
            return response;
        }, error => { // 응답이 에러인 경우에 미리 전처리할 수 있다.
            /**
             * 토큰이 만료되어 401을 리턴하면 발생하면 accessToken을 새로 발급 받고 재요청 한다.
             */
            if (error.response.status === 401) {
                const originalRequest = error.config;
                return accessToken().then((response) => {
                    const refreshToken = response.data;
                    store.commit('authStore/ACCESS_TOKEN', refreshToken);
                    originalRequest.headers.Authorization = store.getters["authStore/userToken"];

                    // token을 새로 발급받으면 새토큰으로 원래 요청을 다시 요청한다.
                    return axios(originalRequest);
                }).catch(() => window.location.replace("/authn/login?targetUrl=" + window.location.href));
            }

            return Promise.reject(error);
        });
```


#### 출처
https://hydev.tistory.com/3