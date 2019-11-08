# cordova-plugin-app-update
App updater for Cordova/PhoneGap forked from  https://github.com/vaenow/cordova-plugin-app-update

# Demo 
Try it yourself:

Just clone and install this demo.
[cordova-plugin-app-update-DEMO](https://github.com/vaenow/cordova-plugin-app-update-demo)
:tada:
 
# Features

Based on the original project 'cordova-plugin-app-update', we add the install API to download the apk and install it imedialitely after donwload finished.

因为有时候我不想用原生的Dialog显示更新的内容，有时候我们的后端开发API人员，检查更新的逻辑和返回数据的格式存在不确定性，所以希望直接能从后端开发人员返回的更新地址中直接下载然后安装更新包。

# Install

### Latest published version on npm (with Cordova CLI >= 5.0.0) 

> `"cordova-android": "6.3.0"`

**从指定git仓库安装**

`cordova plugin add https://github.com/DiclZYY/cordova-plugin-app-update.git --save`

## Usage

```js
window.AppUpdate.ccInstall(null, 失败回调, 新版本信息的对象, 选项对象)
```

- 成功回调
> 下载成功后直接进入安装界面了，无需成功回调

- 失败回调
```js
function(err){
    // err 返回失败对象 {code:'', msg:''}
}

```
- 新版本信息对象
> 传入到原生Android端的参数

```js
{
    version:'', // 新版本版本号(versionCode)，如： 2108， 由于在JS端就比对过，这里留空也不影响 [可选]
    name:'apk_name', // apk文件的本地保存名称，可以自定义，不设定的话会自动取apk的名称 [可选]
    url:'', // 新版本apk文件的地址，[必须]
}

```

栗子：

```js
 if (window.AppUpdate) {
    window.AppUpdate.ccInstall(
      msg => {
        console.info("update app success", msg);
      },
      err => {
        alert(err.code + ":" + err.msg);
        console.error("update app error", err);
      }, {
        // version_code 和 packageUrl在自己的接口中已经取回，这里传入即可
        version: version_code, // 该参数传入无用，因为已经在webview层面进行了版本比对
        name: "ljnewmap_hiking", // 应用名称，下载的apk文件保存到本地的文件名
        url: packageUrl
      }
    );
  } else {
    alert("请使用Andriod设备调试更新功能");
  }
```



