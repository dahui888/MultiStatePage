<p align="center">
    <img align="center" alt="MultiStatePage" src="/imgs/background.png" />
</p>

# MultiStatePage

[![](https://jitpack.io/v/Zhao-Yan-Yan/MultiStatePage.svg)](https://jitpack.io/#Zhao-Yan-Yan/MultiStatePage)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://github.com/Zhao-Yan-Yan/MultiStatePage/blob/master/LICENSE) 
![](https://img.shields.io/badge/language-kotlin-orange.svg)

## 下载Demo

点击或者扫描二维码下载

[![QR code](http://note.youdao.com/yws/public/resource/337a20d817085d4975aca9fd6a381d7c/xmlnote/791CA9D271194A4794BA9E682617C108/6391)](https://www.pgyer.com/1uvC)

| [Activity](app/src/main/java/com/zy/multistatepage/MultiStateActivity.kt) | [Fragment](app/src/main/java/com/zy/multistatepage/MultiFragmentActivity.kt) | [View](app/src/main/java/com/zy/multistatepage/MultiViewActivity.kt) | [ViewPager2](app/src/main/java/com/zy/multistatepage/ViewPager2Activity.kt) |
| :-----: | :----: | :----: | :----: |
| ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c130b72ecd32467daa81ba01a1cd1104~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/26850300b75c45f5b3492826bb9d679e~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/89817b91a608459489135b09a32a48ef~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4b7999fc47124157a2343740ef7280cb~tplv-k3u1fbpfcp-zoom-1.image) |

| [Lottie拓展（自定义State）](app/src/main/java/com/zy/multistatepage/LottieExtActivity.kt) | [State刷新](app/src/main/java/com/zy/multistatepage/RefreshStateActivity.kt) | [网络请求](app/src/main/java/com/zy/multistatepage/MockNetActivity.kt) | [sample](app/src/main/java/com/zy/multistatepage/ApiActivity.kt) |
| :-----: | :----: | :----: | :-----: |
| ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a7501637d9b34814954384cc3a8956e3~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4135913938b349b7993284d394107248~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0fc57adc96dd42ea9e527ae22c61698d~tplv-k3u1fbpfcp-zoom-1.image) | ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ca7768654fc4f1eb68e4becc39c854c~tplv-k3u1fbpfcp-zoom-1.image) |

## MultiStatePage的功能及特点
- 无需在布局添加视图代码
- 可显示自定义状态视图,任意拓展
- 可用于 Activity、Fragment、或指定的 View
- 自定义重新请求监听
- 可动态更新视图样式
- 可结合第三方控件使用
- 支持状态回调监听
- kotlin开发更易用的API

## 开始

### 添加依赖
Step1. Add the JitPack repository to your build file
```
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```

Step2. Add the dependency
[![](https://jitpack.io/v/Zhao-Yan-Yan/MultiStatePage.svg)](https://jitpack.io/#Zhao-Yan-Yan/MultiStatePage)
```
dependencies {
    implementation 'com.github.Zhao-Yan-Yan:MultiStatePage:1.0.9'
}
```
### 1.生成MultiStateContainer

#### 在View上使用
##### kotlin
基础用法
```kotlin
val multiStateContainer = MultiStatePage.bindMultiState(view)

val multiStateContainer = MultiStatePage.bindMultiState(view) { multiStateContainer: MultiStateContainer ->
    // 重试事件处理
}
```
拓展方法
```kotlin
val multiStateContainer = view.bindMultiState()

val multiStateContainer = view.bindMultiState() { multiStateContainer: MultiStateContainer ->
    // 重试事件处理
}
```

##### java
```java
MultiStateContainer multiStateContainer = MultiStatePage.bindMultiState(view)

MultiStateContainer multiStateContainer = MultiStatePage.bindMultiState(view, new OnRetryEventListener() {
    @Override
    public void onRetryEvent(MultiStateContainer multiStateContainer) {
        // 重试事件处理
    }
});
```
#### 在Activity 根View中使用
##### kotlin
基础用法
```kotlin
val multiStateContainer = MultiStatePage.bindMultiState(this)

val multiStateContainer = MultiStatePage.bindMultiState(this) { multiStateContainer: MultiStateContainer ->
    // 重试事件处理
}
```
拓展方法
```kotlin
val multiStateContainer = bindMultiState()

val multiStateContainer = bindMultiState() { multiStateContainer: MultiStateContainer ->
    // 重试事件处理
}
```
##### java
```java
MultiStateContainer multiStateContainer = MultiStatePage.bindMultiState(this);

MultiStateContainer multiStateContainer = MultiStatePage.bindMultiState(this, new OnRetryEventListener() {
    @Override
    public void onRetryEvent(MultiStateContainer multiStateContainer) {
        // 重试事件处理   
    }
});
```
#### 在Fragment根View中使用
##### kotlin
```kotlin
class MultiStateFragment : Fragment {
    
    private lateinit var multiStateContainer: MultiStateContainer
    
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        val root = inflater.inflate(R.layout.fragment, container, false)
        multiStateContainer = MultiStatePage.bindMultiState(root) { multiStateContainer: MultiStateContainer ->
            // 重试事件处理
        }
        //或者
        multiStateContainer = root.bindMultiState() { multiStateContainer: MultiStateContainer ->
            // 重试事件处理
        }
        return multiStateContainer
    }
}
```
##### java
```java
class JavaFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View root = inflater.inflate(R.layout.activity_main, container, false);
        MultiStateContainer multiStateContainer = MultiStatePage.bindMultiState(root);
        return multiStateContainer;
    }
}
```

### 2.切换状态
**调用  `MultiStateContainer.show<T>()` 方法**

**默认内置3种状态**

```kotlin
val multiStateContainer = MultiStatePage.bindMultiState(view)
//成功页 
multiStateContainer.show<SuccessState>()
//错误页
multiStateContainer.show<ErrorState>()
//空页面
multiStateContainer.show<EmptyState>()
//加载状态页
multiStateContainer.show<LoadingState>()
```

**1.1.0新增 `show(multiState: MultiState)`**

```kotlin
val lottieOtherState = LottieOtherState()
lottieOtherState.retry = {
	Toast.makeText(this, "retry...", Toast.LENGTH_SHORT).show()
}
multiStateContainer.show(lottieOtherState)
```

#### 动态设置state

```kotlin
multiStateContainer.show<ErrorState>{errorState ->
    errorState.setErrorMsg("xxx出错了")
}
```

#### 设置重试回调

```kotlin
val multiStateContainer = MultiStatePage.bindMultiState(view){
    Toast.makeText(context, "retry", Toast.LENGTH_SHORT).show()
}
```

### 自定义State
#### 1.继承`MultiState`
```kotlin
class LottieWaitingState : MultiState() {
    override fun onCreateMultiStateView(
        context: Context,
        inflater: LayoutInflater,
        container: MultiStateContainer
    ): View {
        return inflater.inflate(R.layout.multi_lottie_waiting, container, false)
    }

    override fun onMultiStateViewCreate(view: View) {
        //逻辑处理
    }
    
    //是否允许重试
    override fun enableReload(): Boolean = false
    
    //指定重试 view
    override fun bindRetryView(): View? {
        return retryView
    }
}
```
`enableReload()` 是否允许`retry`回调 `false`不允许

`bindRetryView` 绑定重试点击事件的`view` 默认为根`view`

结合`ViewBidng` 参考 `demo` [MultiStateBinding](app/src/main/java/com/zy/multistatepage/base/MultiStateBinding.kt) 和 [WithBindingState](app/src/main/java/com/zy/multistatepage/state/WithBindingState.kt)

#### 2.show (1.0.3后无需register)

```kotlin
class LottieExtActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val multiStateContainer = bindMultiState()
        multiStateContainer.show<LottieWaitingState>()
    }
}
```

### 使用内置状态配置

```kotlin
class App : Application() {
    override fun onCreate() {
        super.onCreate()
        val config = MultiStateConfig.Builder()
            .alphaDuration(300)
            .errorIcon(R.mipmap.state_error)
            .emptyIcon(R.mipmap.state_empty)
            .emptyMsg("emptyMsg")
            .loadingMsg("loadingMsg")
            .errorMsg("errorMsg")
            .build()
        MultiStatePage.config(config)
    }
}
```
| method | 作用 |
| :-----: | :----: |
| `alphaDuration` | alpha动画时长 |
| `errorIcon` | 错误状态默认图标 |
| `emptyIcon` | 空数据状态默认图标 |
| `emptyMsg` | 空数据状态默认提示信息 |
| `errorMsg` | 错误状态默认提示信息 |
| `loadingMsg` | loading状态默认提示信息 |

### 小技巧
可以借助kotlin的拓展函数封装常用的状态
```kotlin
fun MultiStateContainer.showSuccess(callBack: (SuccessState) -> Unit = {}) {
    show<SuccessState> {
        callBack.invoke(it)
    }
}

fun MultiStateContainer.showError(callBack: (ErrorState) -> Unit = {}) {
    show<ErrorState> {
        callBack.invoke(it)
    }
}

fun MultiStateContainer.showEmpty(callBack: (EmptyState) -> Unit = {}) {
    show<EmptyState> {
        callBack.invoke(it)
    }
}

fun MultiStateContainer.showLoading(callBack: (LoadingState) -> Unit = {}) {
    show<LoadingState> {
        callBack.invoke(it)
    }
}
```

调用
```kotlin
val multiStateContainer = bindMultiState()
multiStateContainer.showLoading()
multiStateContainer.showSuccess()
```
## 更新日志
- 1.1.0(2021/01/04) 新增`show(multiState: MultiState)`
- 1.0.9(2020/12/24) demo 包名调整 `enableReload`不强制实现,默认`false`
- 1.0.8(2020/12/09) 修复`LinearLayout`权重异常
- 1.0.7(2020/11/26) 小优化 移除部分`log`打印
- 1.0.6(2020/11/06) 优化`state`切换策略 保留原`view`
- 1.0.5(2020/11/04) `kotlin`函数类型参数更换为`java interface`对`java`的调用更友好
- 1.0.4(2020/11/04) api重命名 `Activity`和`View`统一为`bindMultiState()`
- 1.0.3(2020/10/26) 修复`state`内存泄漏, 移除`register`函数
- 1.0.2(2020/10/23) 支持指定重试`view`, 支持`ViewBinding` 
- 1.0.1(2020/09/22) 支持内置状态页信息配置, 支持`alpha`动画时长配置

## Thanks
- [DylanCaiCoding/LoadingHelper](https://github.com/DylanCaiCoding/LoadingHelper/) 
- [KingJA/LoadSir](https://github.com/KingJA/LoadSir)
- [airbnb/lottie-android](https://github.com/airbnb/lottie-android)
- [lottie动画资源社区](https://lottiefiles.com/featured)
- [玩Android](https://www.wanandroid.com/)

**如果对你有帮助的话可以点个star支持一下子 谢谢亲**

**本项目会长期维护 欢迎issue指正**
## License
```
Copyright (C) 2020. ZhaoYan

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
