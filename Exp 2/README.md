### EXP NO: 02

# Create a simple application client and server service using AIDL interface in android studio.

## AIM:
To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:
Android Studio(Min.required Artic Fox)

## ALGORITHM:

### Step 1: 
Open Android Stdio and then click on File -> New -> New project.

### Step 2: 
Then type the pplication name as CSAIDL and click Next. 

### Step 3: 
Then select the Minimum SDK as shown below and click Next.

### Step 4: 
Then select the Empty Activity and click Next. Finally click Finish.

### Step 5: 
Design layout in activity_main.xml.

### Step 6: 
Display message give in MainActivity file(client/server).

### Step 7: 
Launch an emulator and run the application.

## PROGRAM:
```
Developed by: B.Kavya
Register No.: 212220230007
```

AIDL Server

```
package com.example.aidlserver;
import android.annotation.SuppressLint;
import android.app.Service;
import android.app.Service;
import android.content.Intent;
import android.graphics.Color;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;
import java.util.Random;
public class AIDLColorService extends Service {
    private static final String TAG = "AIDLColorService";
    public AIDLColorService() {
    }
    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.
        return binder;
    }
    private final IAIDLColorinterface.Stub binder = new IAIDLColorinterface.Stub() {
        @Override
        public int getcolor() throws RemoteException {
            Random rnd = new Random();
            int color = Color.argb(255, rnd.nextInt(256), rnd.nextInt(256), rnd.nextInt(256));
            Log.d(TAG, "getColor: "+ color);
            return color;
        }
    }
}
```

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.aidlserver">
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AIDLServer"
        tools:targetApi="31">
        <service
            android:name=".AIDLColorService"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="AIDLColorService"/>
            </intent-filter>
        </service>
    </application>
</manifest>
```

AIDL Client


Activity_Main.xml


```java

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="245dp"
        android:layout_height="273dp"
        android:text="Change the color"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

MainActivity.java

```
package com.example.aidlclient;
import androidx.appcompat.app.AppCompatActivity;
import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import com.example.aidlclient.R;
import com.example.aidlserver.IAIDLColorinterface;

public class MainActivity extends AppCompatActivity {
    IAIDLColorinterface iADILColorService;
    private static final String TAG ="MainActivity";
    private ServiceConnection mConnection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            iADILColorService = IAIDLColorinterface.Stub.asInterface(iBinder);
            Log.d(TAG, "Remote config Service Connected!!");
        }
        @Override
        public void onServiceDisconnected(ComponentName componentName) {
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Intent intent = new Intent("AIDLColorService");
        intent.setPackage("com.example.aidlserver");
        bindService(intent,mConnection, BIND_AUTO_CREATE);

        // Create an onclick listener to button
        Log.d(TAG, "bindservice called");
        Button b = findViewById(R.id.button);

        b.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                try {
                    int color = iADILColorService.getcolor();
                    view.setBackgroundColor(color);
                } catch (RemoteException e) {
                }
            }
        });
    }
}


```


AndroidManifest.xml


```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.aidlclient">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AIDLClient"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>

```

## <br>OUTPUT
![Screenshot (473)](https://user-images.githubusercontent.com/75243072/200628553-d57d1293-659a-43d9-ba11-4492bfe53b8d.png)


![Screenshot (474)](https://user-images.githubusercontent.com/75243072/200628582-390f2cbc-1dfb-431f-b055-596143400cb5.png)

## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.
