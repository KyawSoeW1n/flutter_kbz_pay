# Flutter KBZPay

A Flutter KBZPay Plugin.

## Installation
```yaml
// github
flutter_kbz_pay:
  git:
    url: https://github.com/KyawSoeW1n/flutter_kbz_pay.git
    ref: main
```
## Platform Configuration
### 🧩 Android Setup
Open android/app/src/main/manifest.xml
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
....
<activity
    android:name="com.kbzbank.payment.sdk.callback.CallbackResultActivity"
    android:theme="@android:style/Theme.NoDisplay"
    android:exported="true" />
....
```
### 🍏 iOS Setup
Edit your iOS app’s Info.plist
```plist
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>kbzpay</string>
</array>
....
```
###  Start Payment
You can start a KBZPay payment using either startPay or instantStartPay.
For startPay, in your dart file,
```dart
FlutterKbzPay.startPay(
  prepayId: prepayId,
  merchCode: merchCode,
  appId: appId,
  urlScheme: 'KbzPayExample', // Only for iOS
  signKey: signKey,
).then((res) {
  print('startPay: $res');
});
....
```
For instantStartPay, in your dart file,
Server response with json format
```json
{
        "buildInfo": "appid=xxxxxxx&merch_code=xxxxx&nonce_str=xxxxx&prepay_id=KBZxxxxx&timestamp=xxxxx",
        "signKey": "xxxxxxxx"
}
```
And use server response
```dart
FlutterKbzPay.instantStartPay(
  buildInfo: buildInfo,
  urlScheme: 'KbzPayExample', // Only for iOS
  signType: 'SHA256', // Example
  signKey: signKey,
).then((res) {
  print('instantStartPay: $res');
});
....
```

### Payment callback
Payment callback, payment completion or payment cancellation, currently there are only two states. The callback parameter is returned as an OpenUrl, as shown below

1：Pay for success，
3：Payment failed, the remaining fields are reserved for later addition。
In your dart file,
```dart
...
FlutterKbzPay.onPayStatus().listen((String data) {
      print('onPayStatus $data');
});
....
```

## For Development
Please use dev branch

## For Production
Please use main branch

