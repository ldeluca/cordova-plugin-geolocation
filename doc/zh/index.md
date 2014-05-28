<!---
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->

# org.apache.cordova.geolocation

这个插件提供了有关该设备的位置，例如纬度和经度信息。 常见的位置信息来源包括全球定位系统 (GPS) 和网络信号，如 IP 地址、 RFID、 WiFi 和蓝牙 MAC 地址和 GSM/CDMA 单元格 Id 从推断出的位置。 没有任何保证该API 返回设备的实际位置。

此 API 是基于[W3C Geolocation API Specification][1]，并只执行还没有提供实现的设备上。

 [1]: http://dev.w3.org/geo/api/spec-source.html

**WARNING**： 地理定位数据的收集和使用提出了重要的隐私问题。 您的应用程序的隐私策略应该讨论这款应用程序如何使用地理定位数据，数据是否共享它的任何其他同类的和数据精确程度 （例如，粗、 细，ZIP 代码级别，等等） 。 地理定位数据普遍被认为是敏感的，因为它能揭示用户的行踪，以及他们的行程史的存储。 因此，除了应用程序的隐私策略，您应强烈考虑之前应用程序访问地理定位数据提供的一个时间通知（如果设备操作系统已经不会这样做的话） 。 该通知应提供以上提到的相同的信息，以及获取该用户的权限 （例如，通过**OK**和**No Thanks**提出的选择）。 有关详细信息，请参阅隐私指南。

## 安装

    cordova plugin add org.apache.cordova.geolocation
    

## 支持的平台

*   亚马逊火 OS
*   Android 系统
*   黑莓 10
*   火狐浏览器操作系统
*   iOS
*   Tizen
*   Windows Phone 7 和 8
*   Windows 8

## 方法

*   navigator.geolocation.getCurrentPosition
*   navigator.geolocation.watchPosition
*   navigator.geolocation.clearWatch

## 对象 （只读）

*   Position
*   PositionError
*   Coordinates

## navigator.geolocation.getCurrentPosition

返回设备的当前位置到 `geolocationSuccess` 回调与 `Position` 对象作为参数。 如果有错误， `geolocationError` 回调通过 `PositionError` 对象。

    navigator.geolocation.getCurrentPosition （geolocationSuccess，[geolocationError] [geolocationOptions]) ；
    

### 参数

*   **geolocationSuccess**： 传递当前位置的回调。

*   **geolocationError**： *(Optional)*如果错误发生时则执行回调。

*   **geolocationOptions**： *(Optional)*地理定位选项。

### 示例

    onSuccess 回调 / / 此方法接受一个位置的对象，它包含 / / 目前的 GPS 坐标 / / var onSuccess = function(position) {警报 (' 纬度： '+ position.coords.latitude + \n +' 经度： '+ position.coords.longitude + '\n' +' 海拔高度： '+ position.coords.altitude + \n +' 准确性： '+ position.coords.accuracy + '\n' +' 海拔高度准确性： '+ position.coords.altitudeAccuracy + '\n' +' 标题： '+ position.coords.heading + \n +' 速度： '+ position.coords.speed + '\n' +' 时间戳： ' + position.timestamp + \n) ；} ；onError 回调接收一个 PositionError 对象 / / 函数 onError(error) {警报 (' 代码： '+ error.code + '\n' +' 消息： ' + error.message + \n);}navigator.geolocation.getCurrentPosition (onSuccess，onError) ；
    

## navigator.geolocation.watchPosition

当检测到更改位置返回该设备的当前的位置。 当设备中检索一个新的位置， `geolocationSuccess` 回调执行与 `Position` 对象作为参数。 如果有错误， `geolocationError` 回调执行与 `PositionError` 对象作为参数。

    var watchId = navigator.geolocation.watchPosition （geolocationSuccess，[geolocationError] [geolocationOptions]) ；
    

### 参数

*   **geolocationSuccess**： 传递当前位置的回调。

*   **geolocationError**： (Optional) 如果错误发生时执行的回调。

*   **geolocationOptions**： (Optional) 地理定位选项。

### 返回

*   **字符串**： 返回引用的观看位置间隔的表 id。 应与一起使用的表 id `navigator.geolocation.clearWatch` 停止了观看中位置的更改。

### 示例

    onSuccess 回调 / / 此方法接受一个 '立场' 对象，其中包含 / / 当前 GPS 坐标 / / 函数 onSuccess(position) {var 元素 = document.getElementById('geolocation') ；element.innerHTML = '纬度:' + position.coords.latitude + '< br / >' +' 经度: '+ position.coords.longitude +' < br / >' + ' < hr / >' + element.innerHTML;} / / onError 回调接收一个 PositionError 对象 / / 函数 onError(error) {警报 (' 代码： '+ error.code + '\n' +' 消息： ' + error.message + \n);}如果没有更新收到每隔 30 秒选项： 将引发错误。
    var watchID = navigator.geolocation.watchPosition （onSuccess，onError，{超时： 30000});
    

## geolocationOptions

若要自定义的地理定位检索的可选参数`Position`.

    {maximumAge: 3000，超时： 5000，enableHighAccuracy: true} ；
    

### 选项

*   **enableHighAccuracy**： 提供应用程序需要最佳的可能结果的提示。 默认情况下，该设备将尝试使用基于网络的方法去检索 `Position` 。 将此属性设置为 `true`来告诉此框架要使用更精确的方法，如卫星定位。 *(Boolean)*

*   **超时**： 时间 (毫秒) 从调用传递，允许的最大长度 `navigator.geolocation.getCurrentPosition` 或 `geolocation.watchPosition` 直到相应的 `geolocationSuccess` 回调执行。 如果 `geolocationSuccess` 回调函数不会在此时间内被调用的话， `geolocationError` 回调函数将一个 `PositionError.TIMEOUT` 错误代码。 (请注意，在与 `geolocation.watchPosition`一起使用时 ，`geolocationError` 的回调以每 `timeout` 毫秒的时间间隔来调用)*(Number)*

*   **maximumAge**： 接受一个其老化不超过以毫秒为单位的指定时间的缓存位置。*(Number)*

### Android 的怪癖

Android 2.x 仿真器不返回地理定位结果除非 `enableHighAccuracy` 选项设置为`true`.

## navigator.geolocation.clearWatch

再看对所引用的设备的位置更改为 `watchID` 参数。

    navigator.geolocation.clearWatch(watchID) ；
    

### 参数

*   **watchID**： `watchPosition` 间隔清除的id。(String)

### 示例

    选项： 监视的更改的位置，并使用最 / / 准确定位采集方法可用。
    var watchID = navigator.geolocation.watchPosition （onSuccess，onError，{enableHighAccuracy: true});....later 上的......
    
    navigator.geolocation.clearWatch(watchID) ；
    

## Position

包含 `Position` 坐标和时间戳，由地理位置 API 创建。

### 属性

*   **coords**： 一组地理坐标。*(Coordinates)*

*   **timestamp**： 为 `coords`创建时间戳 。*(Date)*

## Coordinates

A `Coordinates` 对象附加到 `Position` 对象，可用于在当前职位的请求中的回调函数。 它包含一组属性，描述位置的地理坐标。

### 属性

*   **lotitude**： 纬度以十进制度为单位。*(Number)*

*   **longitude**: 经度以十进制度为单位。*(Number)*

*   **altitude**： 位置的高度在椭圆面上以米为单位。*(Number)*

*   **accuracy**：纬度和经度水平坐标的准确性以米来衡量。*(Number)*

*   **altitudeAccuracy**： 海拔高度坐标的精确度以米来衡量。*(Number)*

*   **heading**： 旋转方向，以度为单位，顺时针方向旋转相当于指定正北方向。*(Number)*

*   **speed**： 当前地面设备的speed，指定米/每秒。*(Number)*

### 亚马逊火 OS 怪癖

**altitudeAccuracy**: 不支持的 Android 设备，返回`null`.

### Android 的怪癖

**altitudeAccuracy**: 不支持 Android 设备，返回`null`.

## PositionError

`PositionError`对象传递给 `geolocationError` 与 navigator.geolocation 发生错误时的回调函数。

### 属性

*   **代码**： 下面列出的预定义的错误代码之一。

*   **message**： 描述错误的详细信息的错误讯息遇到的问题。

### 常量

*   `PositionError.PERMISSION_DENIED` 
    *   返回当用户不允许应用程序检索的位置信息。这是取决于平台。
*   `PositionError.POSITION_UNAVAILABLE` 
    *   返回设备时，不能检索的位置。一般情况下，这意味着该设备未连接到网络或无法获取卫星的修复。
*   `PositionError.TIMEOUT` 
    *   返回设备时，无法在指定的时间内检索位置 `timeout` 中包含 `geolocationOptions` 。 与一起使用时 `navigator.geolocation.watchPosition` ，此错误可能反复传递给 `geolocationError` 回调每 `timeout` 毫秒为单位）。