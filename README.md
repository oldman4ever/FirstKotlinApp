# FirstKotlinApp
# FirstKotlinApp
### 1.创建一个新的kotlin工程：
Projects>New Project，选择Basic Activity.语言选择kotlin，并命名工程。
	然后选择模拟机并运行，结果如下：
	
![1](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/1.png)

	
### 2.修改属性:
打开res>layout>fragment_first.xml，首先修改：android:text="@string/hello_first_fragment".
然后右键GO TO>Declaration or Usages,修改如下代码：" <name="hello_first_fragment">Hello first fragment 改为 “Hello Kotlin!”"然后修改属性，最终可以看到代码为：

android:fontFamily="sans-serif-condensed"
android:text="@string/hello_first_fragment"
android:textColor="@android:color/darker_gray"
android:textSize="30sp"
android:textStyle="bold"

运行结果如下：

![2](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/2.png)

### 3.添加按钮和约束：
从Palette面板中拖动Button到如下位置：

![3](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/3.png)

然后调整约束app:layout_constraintTop_toBottomOf="@+id/textview_first" /> 并将id改为:toast_botton.

接下来删除next按键的上约束和左约束。修改组件的文本：

<Button
   android:id="@+id/toast_button"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="Button"
   
在"text" 右键选择Extract string resource。
将resource name 改为 toast_button_text，
value改为：Toast。 Rename 将button_first 改为 random_button.在string.xml文件，右键next字符串资源，选择 Refactor > Rename，修改资源名称为random_button_text，点击Refactor 。随后，修改Next值为Random.添加第三个按钮，位于Toast和Random按钮之间，TextView的下方。新Button的左右约束分别约束至Toast和Random，Top约束至TextView的底部，Buttom约束至屏幕的底部.

最终的fragment_first.xml代码为：

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".FirstFragment">

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-condensed"
        android:text="@string/hello_first_fragment"
        android:textColor="@android:color/darker_gray"
        android:textSize="30sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/random_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />

    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/toast_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />

    <Button
        android:id="@+id/count_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/count_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />
</androidx.constraintlayout.widget.ConstraintLayout>

此时运行会出错，应该进行以下修改，如下图：


![4](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/4.png)

![5](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/5.png)

最终结果如下图：
![13](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/13.png)

### 4.更新按钮和文本框的外观
首先添加一组颜色，如图：

![6](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/6.png)

接下来设置外观：fragment_first.xml中android:background="@color/screenBackground"。android:background="@color/buttonBackground"。并且移除textview的背景颜色，字体大小改为72sp。
然后Toast与屏幕的左边距设置为24dp，Random与屏幕的右边距设置为24dp并：app:layout_constraintVertical_bias="0.3"，左约束改为30.

最终截图如下：
![7](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/7.png)

### 5.添加代码完成交互。
首先设置代码自动补全：在setting中查找Auto Import
并修改如下图：

![8](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/8.png)

TOAST按钮添加一个toast消息：在FirstFragment.kt文件中的onviewCreated加入如下代码：binding.randomButton.setOnClickListener {
    findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
}

再为TOAST按钮添加事件，代码如下：
view.findViewById<Button>(R.id.toast_button).setOnClickListener {
   // create a Toast with some text, to appear for a short time
   val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
   // show the Toast
   myToast.show()
}

### 6.用count按钮更新屏幕的数字。
在FirstFragment.kt文件，为count_buttion按钮添加事件：
view.findViewById<Button>(R.id.count_button).setOnClickListener {
   countMe(view)
}

countme（）：

private fun countMe(view: View) {
   // Get the text view
   val showCountTextView = view.findViewById<TextView>(R.id.textview_first)

   // Get the value of the text view.
   val countString = showCountTextView.text.toString()

   // Convert value to a number and increment it
   var count = countString.toInt()
   count++

   // Display the new value in the text view.
   showCountTextView.text = count.toString()
}

### 7.第二界面代码
在界面添加textview显示随机数：fragment_second.xml的设计视图中去点两个按键间的约束。拖动新的TextView至屏幕的中间位置，用来显示随机数，设置id为@+id/textview_random设置新的TextView的左右约束至屏幕的左右侧，Top约束至textview_second的Bottom，Bottom约束至Button的Top，设置TextView的字体颜色textColor属性@android:color/white，textSize为72sp，textStyle为bold，
设置TextView的显示文字为“R”，
layout_constraintVertical_bias为0.45。
属性代码如下：

<TextView
   android:id="@+id/textview_random"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="R"
   android:textColor="@android:color/white"
   android:textSize="72sp"
   android:textStyle="bold"
   app:layout_constraintBottom_toTopOf="@+id/button_second"
   app:layout_constraintEnd_toEndOf="parent"
   app:layout_constraintStart_toStartOf="parent"
   app:layout_constraintTop_toBottomOf="@+id
   /textview_second"
   app:layout_constraintVertical_bias="0.45" />
截图如下：

![9](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/9.png)

### 8.更新显示界面文本的textview
更改extview_second文本框id为：textview_header，layout_width为match_parent，layout_height为wrap_content。top，left和right的margin为24dp，colors.xml添加颜色colorPrimaryDark，并将TextView颜色设置为@color/colorPrimaryDark，字体大小为24sp。strings.xml文件中，修改hello_second_fragment的值为"Here is a random number between 0 and %d."Refactor>Rename将hello_second_fragment 重构为random_heading。
最终代码如下：
<TextView
   android:id="@+id/textview_header"
   android:layout_width="0dp"
   android:layout_height="wrap_content"
   android:layout_marginStart="24dp"
   android:layout_marginLeft="24dp"
   android:layout_marginTop="24dp"
   android:layout_marginEnd="24dp"
   android:layout_marginRight="24dp"
   android:text="@string/random_heading"
   android:textColor="@color/colorPrimaryDark"
   android:textSize="24sp"
   app:layout_constraintEnd_toEndOf="parent"
   app:layout_constraintStart_toStartOf="parent"
   app:layout_constraintTop_toTopOf="parent" />

### 9.更改界面的背景色和按钮布局
color.xml添加颜色：
color name="screenBackground2">#26C6DA</color>,并将其修改为fragment_second.xml背景色。

### 10.启用SafeArgs
Gradle的Project部分，在plugins节添加：
id 'androidx.navigation.safeargs.kotlin' version '2.5.0-alpha01' apply false。
module部分在plugins节添加:
id 'androidx.navigation.safeargs'.
### 11.创建导航动作参数
打开导航视图，点击FirstFragment，查看其属性。
在Actions栏中可以看到导航至SecondFragment

同理，查看SecondFragment的属性栏
点击Arguments **+**符号
弹出的对话框中，添加参数myArg，类型为整型Integer。如下图：

![11](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/11.png)

### 12.FirstFragment添加代码，向SecondFragment发数据
在FirstFragment.kt中：
val showCountTextView = view.findViewById<TextView>(R.id.textview_first)

val currentCount = showCountTextView.text.toString().toInt()

将currentCount作为参数传递给actionFirstFragmentToSecondFragment()：
val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCoun）

添加导航代码：
findNavController().navigate(action)

### 13.添加SecondFragment的代码
加入以下代码：
import androidx.navigation.fragment.navArgs

onViewCreated()中获取传递过来的参数列表，提取count数值，并在textview_header中显示
val args: SecondFragmentArgs by navArgs()：
val count = args.myArg

val countText = getString(R.string.random_heading, count)

view.findViewById<TextView>(R.id.textview_header).text = countText

根据count值生成随机数

val random = java.util.Random()

var randomNumber = 0

if (count > 0) {
   randomNumber = random.nextInt(count + 1)
}

textview_random中显示count值：
view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()

最终结果如下图：

![12](https://github.com/oldman4ever/FirstKotlinApp/blob/master/screenshot/12.png)
   
   
