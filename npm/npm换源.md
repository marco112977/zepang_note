### 由于不可说原因，npm install时，速度总是不尽如人意，解决办法是修改npm的数据源
~~~shell
npm config set registry https://registry.npm.taobao.org
~~~
### 修改后可以通过这个进行测试
~~~shell
npm config get registry
~~~

### 临时使用 
~~~shell
npm install package -g --registry https://registry.npm.taobao.org
~~~

### windows 端口占用

```
netstat -ano|findstr "8000"
tskill 1234
```


# yarn 换源

```shell
# 查看源
yarn config get registry
# 淘宝源
yarn config set registry https://registry.npm.taobao.org
# 自带源
yarn config set registry https://registry.yarnpkg.com
```