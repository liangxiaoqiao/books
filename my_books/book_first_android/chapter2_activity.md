### Activity

####  创建Activity
1. 手动创建一个Activity类（不选择 Generate Layout 和 Launcher Activity， 后边手动配置）
2. 创建res文件夹下的layout文件，同时在Activity类的onCreate方法，调用setContentView()用来加载布局
3. AndroidMainfest文件中注册Activity活动
    ```xml
        <activity android:name=".FirstActivity">
            <intent-filter>
                <!-- 新加下边的两行，注册为启动器 -->
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    ```
#### 使用Toast
1. findViewById 找到创建的Button
2. button.setOnClickListener 注册点击事件
3. 事件中调用Toast.makeText创建一个提示文本，当点击button的时候，就会显示提示文本

#### 使用Menu
1. 首先需要在menu的文件夹创建menu的xml文件
2. 在Activity的class中重写 onCreateOptionsMenu方法，使用menuInflater.inflate(R.menu.main, menu)来加载menu
3. 在Activity的class中重写 onOptionsItemSelected方法，可以根据每个MenuItem的ItemId找到对应的每一个menu，然后响应不同的注册事件

#### 使用Intent
1. 显式调用Intent
    ```kotlin
        //启动一个指定的Activity
        val intent = Intent(this,TargetActivity::class)
        startActivity(intent)
    ```
2. 隐式调用Intent
    ```kotlin
        //mainfest文件中配置了
        //<action android:name="action_str"/>
        //<category android:name="com.example.demo.MY_CATEGORY"/>
        //的Activity才会响应。（不addCategory，intent默认会自己调用addCategory("android.intent.category.DEFAULT")）
        val intent = Intent("action_str")
        intent.addCategory("com.example.demo.MY_CATEGORY")
        startActivity(intent)
        //打开浏览器
        val intent = Intent(Intent.ACTION_VIEW)
        intent.data = Uri.parse("http://www.baidu.com")
        startActivity(intent)
        //拨号
        val intent = Intent(Intent.ACTION_DIAL)
        intent.data = Uri.parse("tel:10010")
        startActivity(intent)
    ```
3. mainfest中，action只能配置一个，而category可以配置多个。\<data>标签可以更精确的指定匹配：例如 scheme  host port path mimeType等
4. Intent通过putExtra方法传递数据，在目标Intent调用 get方法根据相同key获取传递的值
5. Intent返回数据
    1. 源Activity调用startActivityForResult方法，启动另一个活动，同时等待获取返回值（设置唯一的requestCode）
    2. 目标Activity调用setResult把带有数据的Intent返回回去（可以通过onClick调用finish方法，或者重写onBackPressed：按下返回键时触发）
    3. 目标Activity销毁之后，会回调 源Activity的onActivityForResult方法
    4. 重写该方法，从Intent获取返回的数据（参数requestCode resultCode intent）

#### 活动的生命周期
1. 返回栈
    每个Activity都会压入栈中，栈顶就是看到的Activity
1. 七个周期
    1. onCreate
    2. onStart
    3. onResume
    4. onPause
    5. onStop
    6. onDestory
    7. onRestart
2. 每个周期的调用时间
3. 活动回收怎么办哪
     ```
    活动在非运行状态，会被虚拟机回收掉，此时如果活动需要restart恢复状态，可以
    1. override onSaveInstanceState 将数据保存到 Bundle当中。
    2. 在重新调用onCreate方法的时候，从入参Bundle中获取保存的信息。
     ```
4. 启动模式
    1. standard 标准模式，默认的。
    2. singleTop 当Activity在栈顶，再次创建只会返回这一个
    3. singleTask 不论Activity在哪里，再次创建只会返回这一个
    4. singleInstance 在一个单独的返回栈中，解决多个应用共享的问题
5. 直接退出 （保存所有Activity，退出时候，直接遍历finish）
