MIT License

Copyright (c) 2018 老九

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
## WebApiClient 　　　　　　　　　　　　　　　　　　　
### 1 Nuget包

> WebApiClient.JIT

    PM> install-package WebApiClient.JIT
* 不适用于不支持JIT技术的平台(IOS、UWP)；
* Http接口声明要求为public；


> WebApiClient.AOT

    PM> install-package WebApiClient.AOT
* 适用于不支持JIT技术的平台(IOS、UWP)；
* Http接口声明不要求为public，可以嵌套在类里面；


### 2. Http请求
> 接口的声明

```c#
public interface IUserApi : IHttpApi
{
    // GET api/user?account=laojiu
    // Return json或xml内容
    [HttpGet("api/user")]
    ITask<UserInfo> GetAsync(string account);

    // POST api/user  
    // Body Account=laojiu&password=123456
    // Return json或xml内容
    [HttpPost("api/user")]
    ITask<boo> AddAsync([FormContent] UserInfo user);
}
```
 
> 接口的配置

```c#
HttpApi.Register<IUserApi>().ConfigureHttpApiConfig(c =>
{
    c.HttpHost = new Uri("http://www.webapiclient.com/");
    c.FormatOptions.DateTimeFormat = DateTimeFormats.ISO8601_WithMillisecond;
});;
```

> 接口的调用

```c#
var api = HttpApi.Resolve<IUserApi>();
var user = new UserInfo { Account = "laojiu", Password = "123456" }; 
var user1 = await api.GetAsync("laojiu");
var state = await api.AddAsync(user);
``` 

#### 3. Api变化
> 相对于[v0.3.6](https://github.com/dotnetcore/WebApiClient/tree/v0.3.6)或以前版本，Api有如下变化 

* ~~HttpApiClient.Create()~~ -> HttpApi.Create()
* ~~HttpApiFactory.Add()~~ -> HttpApi.Register()
* ~~HttpApiFactory.Create()~~ -> HttpApi.Resolve()
* ~~Timeout~~
* ~~UrlAttribute~~
* ~~DebugAttribute~~

#### 4. Wiki文档
1. [WebApiClient基础](https://github.com/xljiulang/WebApiClient/wiki/WebApiClient%E5%9F%BA%E7%A1%80)
2. [WebApiClient进阶](https://github.com/dotnetcore/WebApiClient/wiki/WebApiClient%E8%BF%9B%E9%98%B6)
3. [WebApiClient高级](https://github.com/xljiulang/WebApiClient/wiki/WebApiClient%E9%AB%98%E7%BA%A7)
4. [WebApiClient.Extensions](https://github.com/xljiulang/WebApiClient.Extensions)
5. [WebApiClient.Tools.Swagger](https://github.com/xljiulang/WebApiClient.Tools)

#### 5. 联系方式
1. 加Q群825135345 注明WeApiClient
2. 邮箱366193849@qq.com，不重要的尽量不要发

 本目录的所有类型是外链类型，将参与到编译中；
 给目标程序集插入IL时，目标程序集使用着WebApiClient.AOT.dll中对应本类型的类型