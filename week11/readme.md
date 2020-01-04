### ARTS

#### Algorithm
##### Design Circular Queue
Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Your implementation should support following operations:
* MyCircularQueue(k): Constructor, set the size of the queue to be k.
* Front: Get the front item from the queue. If the queue is empty, return -1.
* Rear: Get the last item from the queue. If the queue is empty, return -1.
* enQueue(value): Insert an element into the circular queue. Return true if the operation is successful.
* deQueue(): Delete an element from the circular queue. Return true if the operation is successful.
* isEmpty(): Checks whether the circular queue is empty or not.
* isFull(): Checks whether the circular queue is full or not.

Example:
```
MyCircularQueue circularQueue = new MyCircularQueue(3); // set the size to be 3
circularQueue.enQueue(1);  // return true
circularQueue.enQueue(2);  // return true
circularQueue.enQueue(3);  // return true
circularQueue.enQueue(4);  // return false, the queue is full
circularQueue.Rear();  // return 3
circularQueue.isFull();  // return true
circularQueue.deQueue();  // return true
circularQueue.enQueue(4);  // return true
circularQueue.Rear();  // return 4
```

```java
class MyCircularQueue {

    private int[] items;
    private int n;
    private int head = 0;
    private int tail = 0;
    private int currentTail = 0;

    /** Initialize your data structure here. Set the size of the queue to be k. */
    public MyCircularQueue(int k) {
        n = k + 1;
        items = new int[n];
    }

    /** Insert an element into the circular queue. Return true if the operation is successful. */
    public boolean enQueue(int value) {
        if ((tail + 1) % n == head) return false;
        currentTail = tail;
        items[currentTail] = value;
        tail = (tail + 1) % n;
        return true;
    }

    /** Delete an element from the circular queue. Return true if the operation is successful. */
    public boolean deQueue() {
        if (head == tail) return false;
        head = (head + 1) % n;
        return true;
    }

    /** Get the front item from the queue. */
    public int Front() {
        return head == tail ? -1 : items[head];
    }

    /** Get the last item from the queue. */
    public int Rear() {
        return head == tail ? -1 : items[currentTail];
    }

    /** Checks whether the circular queue is empty or not. */
    public boolean isEmpty() {
        return head == tail;
    }

    /** Checks whether the circular queue is full or not. */
    public boolean isFull() {
        return (tail + 1) % n == head;
    }
}


/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
```

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