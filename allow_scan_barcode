HOW TO ALLOW WEBVIEW TO USE CAMERA AND FILE TO SCAN BARCODE

Add permission in AndroidManifest.xml:
```
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" android:required="true" />
<uses-feature android:name="android.hardware.camera.autofocus" android:required="true" />
<uses-feature android:name="android.hardware.camera.front" android:required="true" />
<uses-feature android:name="android.hardware.camera" android:required="true" />
<uses-feature android:name="android.hardware.camera.level.full" android:required="true" />
<uses-feature android:name="android.hardware.camera.capability.raw" android:required="true" />
<uses-feature android:name="android.hardware.camera.any" android:required="true" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

Add functions in  java > com.[APP_URL] > MainActivity to check if phone already allow these permission if not then ask on app start:
```
    private static final String[] PERMISSION = new String[]{
            Manifest.permission.CAMERA,
            Manifest.permission.READ_EXTERNAL_STORAGE
    };
    private static final int REQUEST_CODE = 10; //number can be anything, this works just like a port

    private boolean hasCameraPermission() {
        return ContextCompat.checkSelfPermission(
                this,
                Manifest.permission.CAMERA
        ) == PackageManager.PERMISSION_GRANTED;
    }
    private boolean hasFilePermission() {
        return ContextCompat.checkSelfPermission(
                this,
                Manifest.permission.READ_EXTERNAL_STORAGE
        ) == PackageManager.PERMISSION_GRANTED;
    }
    private void requestPermission() {
        ActivityCompat.requestPermissions(
                this,
                PERMISSION,
                REQUEST_CODE
        );
    }
```

Call the function at the start of onCreate in java > com.[APP_URL] > MainActivity:
```
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        if (hasCameraPermission() == false || hasFilePermission() == false) {
            requestPermission();
        }

        ...

        webView.setWebChromeClient(new WebChromeClient() {
            @Override
            public void onPermissionRequest(PermissionRequest request) {
                request.grant(request.getResources());
            }
        });
    }
```

Import all the required class:
```
import android.webkit.PermissionRequest;
import android.webkit.WebChromeClient;
import android.Manifest;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import android.content.pm.PackageManager;
```
