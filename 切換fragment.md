
#MainActivity.java

package com.example.cap.myapplication;
import android.app.Activity;
import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.app.Fragment;

public class MainActivity extends Activity {
    Button bn ;
    boolean state = true;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        bn = (Button)findViewById(R.id.bn);
        bn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v)
            {
                FragmentManager fragmentMgr = getFragmentManager();//呼叫getFragmentManager()方法取得FragmentManager。
                FragmentTransaction fragmentTrans = fragmentMgr.beginTransaction();//呼叫FragmentManager的beginTransaction()方法建立一個FragmentTransaction物件。
                Fragment fm ;
                if(state)
                {
                    fm = new BlankFragment1();//建立BlankFragment1類別的fragment
                    fragmentTrans.replace(R.id.container,fm);//用另外一個Fragment取代目前程式畫面中的Fragment.(容器id,要塞入的fragment)
                    fragmentTrans.commit();//開始執行Fragment的切換
                    bn.setText("turn to 2");
                    state = false;
                }
                else
                {
                    fm = new BlankFragment2();
                    fragmentTrans.replace(R.id.container,fm);
                    fragmentTrans.commit();
                    bn.setText("turn to 1");
                    state = true;
                }
            }
        });
    }
}

=====================
# BlankFragment1.java
=====================
package com.example.cap.myapplication;
import android.os.Bundle;
import android.support.v4.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;


public class BlankFragment1 extends android.app.Fragment {


    public BlankFragment1() {
        // Required empty public constructor
    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_blank1, container, false);//透過inflate()方法取得自訂版面,並將View型別物件存於convertView
    }

}

=====================
# BlankFragment2.java
=====================
package com.example.cap.myapplication;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;


public class BlankFragment2  extends android.app.Fragment {

    public BlankFragment2() {
        // Required empty public constructor
    }


    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_blank2, container, false);
    }

}

=====================
# fragment_blank1.xml
=====================
FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="400dp"
    android:background="#8F3A1E"
    tools:context="com.example.cap.myapplication.BlankFragment1">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Fragment 1"
        android:textAppearance="?android:textAppearanceLarge"
        android:layout_gravity="center"
        android:gravity="center"
        android:id="@+id/fragment_blank1"/>

</FrameLayout>

=====================
# fragment_blank2.xml
=====================
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="400dp"
    android:background="@color/colorAccent"
    tools:context="com.example.cap.myapplication.BlankFragment1">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Fragment 2"
        android:textAppearance="?android:textAppearanceLarge"
        android:layout_gravity="center"
        android:gravity="center"/>

</FrameLayout>

=====================
# activity_main.xml
=====================
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:orientation="vertical"
    tools:context="com.example.cap.myapplication.MainActivity">
<Button
    android:layout_width="250dp"
    android:layout_height="wrap_content"
    android:text="Load Fragment1"
    android:layout_gravity="center_horizontal"
    android:id="@+id/bn"/>
<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="400dp"
    android:layout_marginTop="20dp"
    android:id="@+id/container"/>


</LinearLayout>
