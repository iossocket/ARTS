### ARTS

#### Algorithm

#### Review

***SwiftUI by Tutorials*** raywenderlich 发布的一本英文电子书

#### Tips

1. iOS 如何在初始化CBCentralManager时，监测Bluetooth是否开启，并在没有开启Bluetooth的情况下弹出提示框，引导用户进入setting进去操作：
```swift
centralManager = CBCentralManager(delegate: self, queue: nil, options: [CBCentralManagerOptionShowPowerAlertKey: true])
```
2. Android 如何通过代码来开启Bluetooth
```kotlin
val adapter = BluetoothAdapter.getDefaultAdapter()
if (!adapter.isEnabled) {
    val enableBtIntent = Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE)
    startActivityForResult(enableBtIntent, 1)
}

...

override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
    Log.i(TAG, requestCode.toString())
    super.onActivityResult(requestCode, resultCode, data)
}

```
3. Android 如何动态申请权限
```kotlin
if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
    if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.ACCESS_FINE_LOCATION)) {
        val alertBuilder = AlertDialog.Builder(this)
        alertBuilder.setCancelable(true)
        alertBuilder.setTitle("Permission necessary")
        alertBuilder.setMessage("Location permission is necessary")
        alertBuilder.setPositiveButton(android.R.string.yes) { a, b ->
            requestPermissions(arrayOf(Manifest.permission.ACCESS_FINE_LOCATION), 0)
        }
        val alert = alertBuilder.create()
        alert.show()
    } else {
        requestPermissions(arrayOf(Manifest.permission.ACCESS_FINE_LOCATION), 0)
    }
}
...
override fun onRequestPermissionsResult(requestCode: Int, permissions: Array<out String>, grantResults: IntArray) {
    Log.i(TAG, permissions[0])
    Log.i(TAG, grantResults[0].toString())
}

```

#### Sharing

开始重新学backend，开始写一个系列文章：