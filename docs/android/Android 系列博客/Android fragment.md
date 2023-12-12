## 参考文档
https://blog.csdn.net/CongPong/article/details/125919261



## 概念

Fragments必须放在一个Activity中
Fragments可以接收它自己的事件
一个Fragment可以放在多个Activity中，一个Activity中也可以放置多个Fragments
Fragments有它自己的生命周期，而且受到它所在的宿主Activity的生命周期的影响

## 使用案例

```java
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Create a new instance of the SimpleFragment
        SimpleFragment simpleFragment = new SimpleFragment();

        // Get a reference to the FragmentManager
        FragmentManager fragmentManager = getSupportFragmentManager();

        // Begin the transaction
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();

        // Add the SimpleFragment to the container with a unique tag
        fragmentTransaction.add(R.id.fragment_container, simpleFragment, "simple_fragment");

        // Commit the transaction
        fragmentTransaction.commit();
    }
}
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SimpleFragment">

    <TextView
        android:id="@+id/text_view"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!" />

</LinearLayout>

```

```java
import android.os.Bundle;
import android.view.LayoutInflater;   
import android.view.ViewGroup;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;

public class SimpleFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        View view = inflater.inflate(R.layout.fragment_simple, container, false);

        // Add a TextView to display some text
        TextView textView = view.findViewById(R.id.text_view);
        textView.setText("Hello, World!");

        return view;
    }
}

```





## 生命周期

onAttach()                

        当Fragment与Activity建立关联的时候调用，Activity作为参数传入。

onCreate()               

        创建Fragment的时候系统会调用此函数。

onCreateView()       

        创建Fragment的UI.
    
        这个方法必须返回一个View。
    
        表示这个Fragment的根布局。

onActivityCreated()        

        当Activity的onCreate()方法返回时调用。

onStart()                 

        当Fragment第一次绘制它的UI的时候调用。

onResume()

        当Fragment可见且可交互时调用。
onPause()           

        当用户离开当前Fragment时调用这个方法。
        通常用来保存持久化数据。             

onStop()

        当Fragment不可见时调用。可能情况：activity被stopped或fragment被移除，加入到回退栈。一个stopped的fragment任然是活着的，如果长时间不用也会被移除。

onDestroyView()                

        当Fragment的UI被删除的时候调用。

onDestory()

        当Fragment销毁时调用

onDetach()                        

        当Fragment与Activity取消关联的时候调用。



## 