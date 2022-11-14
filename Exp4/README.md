# Ex.No: 4 Develop a simple application to display the available sensor in android mobile devices using Sensor Manager in android studio.


## AIM:

To develop a sensor application to use the sensor manager class to identify and get the list of available sensors on a device in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Arctic Fox)

## ALGORITHM:

### Step 1: 
Open Android Studio and then click on File -> New -> New project.

### Step 2: 
Then type the Application name as Sensor and click Next. 

### Step 3: 
Then select the Minimum SDK as shown below and click Next.

### Step 4: 
Then select the Empty Activity and click Next. Finally click Finish.

### Step 5: 
Design layout in activity_main.xml.

### Step 6: 
Display avaliable sensor in android mobile devices.

### Step 7: 
Launch an emulator and run the application.

## PROGRAM:
```
/*
Program to print the avaliable sensor in android mobile devices.
Developed by        : B.Kavya
Registration Number : 212220230007
*/
```
### MainActivity.java
```
package com.example.sensors;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import java.util.List;

public class MainActivity extends AppCompatActivity {
    private SensorManager mgr;
    private TextView txtList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mgr = (SensorManager)getSystemService(Context.SENSOR_SERVICE);
        txtList = (TextView)findViewById(R.id.sensorslist);
        List<Sensor> sensorList = mgr.getSensorList(Sensor.TYPE_ALL);
        StringBuilder strBuilder = new StringBuilder();
        for(Sensor s: sensorList){
            strBuilder.append(s.getName()+"\n");
        }
        txtList.setVisibility(View.VISIBLE);
        txtList.setText(strBuilder);
    }
}
```
### activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="10dp"
    android:paddingRight="10dp">
    <TextView
        android:id="@+id/sensorslist"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="80dp"
        android:text="Sensors"
        android:textSize="20dp"
        android:textStyle="bold"
        android:layout_gravity="center"
        android:visibility="gone"/>
</LinearLayout>
```

## OUTPUT:
![image](https://user-images.githubusercontent.com/75234991/200128043-f2e0f9ee-c7c7-44ba-a795-40618b3e93de.png)

## RESULT:
Thus, a Simple Android Application to display the avaliable sensor in android mobile devices using Sensor Manager in Android Studio is developed and executed successfully.
