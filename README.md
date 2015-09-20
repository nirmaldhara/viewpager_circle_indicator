# viewpager_circle_indicator
In many android apps we have seen sliding images with circle indicator. This kind of sliding image gallery can be develop using viewpager
,Fallow the below steps to develop sliding image gallery with circle indicator.
##Step1
Create a blank android project using android studio. if you don’t know how to create a project in android, see my [previous post](http://javaant.com/category/android/#.Vf6gKvmqqko).
##Step2
Create three blank fragment for displaying image. you can create as many as you want.
##Step3fragment_image_one.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent" tools:context="com.javamad.ImageOneFragment"
    >

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:src="@drawable/img1"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:id="@+id/imageView" />




</RelativeLayout>

```
##fragment_image_two.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent" tools:context="com.javamad.ImageTwoFragment"
    >

<ImageView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/img2"
    android:layout_centerVertical="true"
    android:layout_centerHorizontal="true" />


</RelativeLayout>
```
##fragment_image_three.xml

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent" tools:context="com.javamad.ImageThreeFragment"
   >

    <ImageView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/img3"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true" />


</RelativeLayout>
```
##Step3
Create a footer.xml to place the circle indicator.
##footer.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    android:layout_height="wrap_content" android:layout_width="match_parent"
    android:orientation="vertical"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_gravity="bottom"
    android:background="#00000000"

    >
    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        >
        <ImageView android:layout_height="10dp" android:layout_width="10dp"
            android:id="@+id/btn1"
            android:src="@drawable/holo_circle"
            android:layout_gravity="center_vertical"

            />

        <ImageView android:layout_height="10dp" android:layout_width="10dp"
            android:id="@+id/btn2"
            android:layout_toRightOf="@id/btn1"
            android:src="@drawable/holo_circle"
            android:layout_margin="10dp"
            />
        <ImageView android:layout_height="10dp" android:layout_width="10dp"
            android:id="@+id/btn3"
            android:layout_toRightOf="@id/btn2"
            android:src="@drawable/holo_circle"
            android:layout_gravity="center_vertical"
            />
    </LinearLayout>
    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:id="@+id/buttonlayout"

        >

        <Button
            android:id="@+id/btnNewUserPopup"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text=" New User "
            android:layout_alignParentLeft="true"
            android:layout_weight=".5"
            />

        <Button
            android:id="@+id/btnSignInPopup"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight=".5"
            android:text="Sign In"
            android:layout_alignParentRight="true"

            />

    </LinearLayout>


</LinearLayout>
```
##Step4
##ImageViewPagerAdapter.java
```java
package javaant.com.viewpager_circle_indicator;

import android.app.Fragment;
import android.app.FragmentManager;
import android.content.Context;
import android.support.v13.app.FragmentPagerAdapter;

/**
 * Created by nirmal on 12/08/15.
 */
public class ImageViewPagerAdapter extends FragmentPagerAdapter {
    private Context _context;
    public static int totalPage = 3;

    public ImageViewPagerAdapter(Context context, FragmentManager fm) {
        super(fm);
        _context = context;

    }

    @Override
    public Fragment getItem(int position) {
        Fragment f = new Fragment();
        switch (position) {
            case 0:
                f = new ImageOneFragment();
                break;
            case 1:
                f = new ImageTwoFragment();
                break;
            case 2:
                f = new ImageThreeFragment();
                break;
        }
        return f;
    }

    @Override
    public int getCount() {
        return totalPage;
    }

}

```
##MainActivityFragment.java
```java
package javaant.com.viewpager_circle_indicator;

import android.app.Fragment;
import android.os.Bundle;
import android.support.v4.view.ViewPager;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.ImageView;

/**
 * A placeholder fragment containing a simple view.
 */
public class MainActivityFragment extends Fragment {
    private ViewPager _mViewPager;
    private ImageViewPagerAdapter _adapter;
    private ImageView _btn1, _btn2, _btn3;
    public MainActivityFragment() {
    }


    @Override
    public void onViewCreated(View view, Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        setUpView();
        setTab();
        onCircleButtonClick();
    }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {

        return inflater.inflate(R.layout.fragment_main, container, false);
    }

    private void onCircleButtonClick() {

        _btn1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                _btn1.setImageResource(R.drawable.fill_circle);
                _mViewPager.setCurrentItem(0);
            }
        });

        _btn2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                _btn2.setImageResource(R.drawable.fill_circle);
                _mViewPager.setCurrentItem(1);
            }
        });
        _btn3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                _btn3.setImageResource(R.drawable.fill_circle);
                _mViewPager.setCurrentItem(2);
            }
        });
    }

    private void setUpView() {
        _mViewPager = (ViewPager) getView().findViewById(R.id.imageviewPager);
        _adapter = new ImageViewPagerAdapter(getActivity(), getFragmentManager());
        _mViewPager.setAdapter(_adapter);
        _mViewPager.setCurrentItem(0);
        initButton();
    }

    private void setTab() {
        _mViewPager.setOnPageChangeListener(new ViewPager.OnPageChangeListener() {

            @Override
            public void onPageScrollStateChanged(int position) {
            }

            @Override
            public void onPageScrolled(int arg0, float arg1, int arg2) {
            }

            @Override
            public void onPageSelected(int position) {
                // TODO Auto-generated method stub
                _btn1.setImageResource(R.drawable.holo_circle);
                _btn2.setImageResource(R.drawable.holo_circle);
                _btn3.setImageResource(R.drawable.holo_circle);
                btnAction(position);
            }

        });

    }

    private void btnAction(int action) {
        switch (action) {
            case 0:
                _btn1.setImageResource(R.drawable.fill_circle);

                break;

            case 1:
                _btn2.setImageResource(R.drawable.fill_circle);

                break;
            case 2:
                _btn3.setImageResource(R.drawable.fill_circle);

                break;
        }
    }

    private void initButton() {
        _btn1 = (ImageView) getView().findViewById(R.id.btn1);
        _btn1.setImageResource(R.drawable.fill_circle);
        _btn2 = (ImageView) getView().findViewById(R.id.btn2);
        _btn3 = (ImageView) getView().findViewById(R.id.btn3);

    }

    private void setButton(Button btn, String text, int h, int w) {
        btn.setWidth(w);
        btn.setHeight(h);
        btn.setText(text);
    }
}
```
