# Purpose Strings Guide for SWI Dashboard App

## المشكلة
Apple يرفض التطبيق لأن purpose strings (نصوص الأذونات) غير واضحة ولا تحتوي على أمثلة محددة.

## الحل المطلوب

### 1. Location Permission (أذونات الموقع) - الأهم

#### ❌ نصوص غير مقبولة (مثل ما لديك الآن):
```
"App needs location access"
"Location permission required"
"SWI Dashboard needs your location"
```

#### ✅ نصوص مقبولة (يجب استخدامها):

**لـ iOS - Info.plist:**

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>SWI Dashboard uses your location to find and display the nearest refrigerators on the map. For example, when you open the map view, the app will show your current position and highlight the closest refrigerator locations within a 5km radius, helping you navigate to the nearest available refrigerator for your operations.</string>

<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>SWI Dashboard uses your location in the background to track your route and optimize operations. For example, when you're visiting multiple refrigerator locations, the app tracks your path to help you complete your route efficiently and record which locations you've visited.</string>
```

**لـ Android - AndroidManifest.xml:**

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

**في كود Flutter (إذا كنت تستخدم Flutter):**

في ملف `android/app/src/main/AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

### 2. Camera Permission (أذونات الكاميرا)

#### ✅ نص مقبول:

**لـ iOS - Info.plist:**
```xml
<key>NSCameraUsageDescription</key>
<string>SWI Dashboard uses your camera to take photos of refrigerators, equipment, or documents. For example, you can take a photo of a refrigerator to document its condition, or capture an image of a document to upload it to the system.</string>
```

### 3. Photo Library Permission (أذونات مكتبة الصور)

#### ✅ نص مقبول:

**لـ iOS - Info.plist:**
```xml
<key>NSPhotoLibraryUsageDescription</key>
<string>SWI Dashboard accesses your photo library to select images for upload. For example, you can choose an existing photo from your library to attach to a report or use as a profile picture.</string>

<key>NSPhotoLibraryAddUsageDescription</key>
<string>SWI Dashboard saves exported images and reports to your photo library. For example, when you export a report as an image or PDF, the app will save it to your Photos app for easy sharing.</string>
```

### 4. Microphone Permission (أذونات الميكروفون)

#### ✅ نص مقبول:

**لـ iOS - Info.plist:**
```xml
<key>NSMicrophoneUsageDescription</key>
<string>SWI Dashboard uses your microphone for voice notes and audio recordings. For example, you can record voice notes while inspecting a refrigerator to document observations hands-free, which will be saved as an audio file attached to your report.</string>
```

## أين يجب تحديث هذه النصوص؟

### لـ iOS (Xcode Project):
1. افتح مشروع Xcode
2. اذهب إلى `ios/Runner/Info.plist` (أو `ios/[AppName]/Info.plist`)
3. أضف أو حدث المفاتيح المذكورة أعلاه

### لـ Flutter:
1. **iOS:** `ios/Runner/Info.plist`
2. **Android:** `android/app/src/main/AndroidManifest.xml`

### لـ React Native:
1. **iOS:** `ios/[AppName]/Info.plist`
2. **Android:** `android/app/src/main/AndroidManifest.xml`

## ملاحظات مهمة:

1. **يجب أن تكون النصوص باللغة الإنجليزية** (أو اللغة الأساسية للتطبيق)
2. **يجب أن تحتوي على مثال محدد** يشرح بالضبط كيف سيتم استخدام البيانات
3. **يجب أن تكون واضحة ومباشرة** - لا تستخدم نصوص عامة
4. **يجب أن تطابق الاستخدام الفعلي** - لا تكتب استخدامات غير موجودة في التطبيق

## مثال كامل لـ Info.plist:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <!-- Location Permissions -->
    <key>NSLocationWhenInUseUsageDescription</key>
    <string>SWI Dashboard uses your location to find and display the nearest refrigerators on the map. For example, when you open the map view, the app will show your current position and highlight the closest refrigerator locations within a 5km radius, helping you navigate to the nearest available refrigerator for your operations.</string>
    
    <key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
    <string>SWI Dashboard uses your location in the background to track your route and optimize operations. For example, when you're visiting multiple refrigerator locations, the app tracks your path to help you complete your route efficiently and record which locations you've visited.</string>
    
    <!-- Camera Permission -->
    <key>NSCameraUsageDescription</key>
    <string>SWI Dashboard uses your camera to take photos of refrigerators, equipment, or documents. For example, you can take a photo of a refrigerator to document its condition, or capture an image of a document to upload it to the system.</string>
    
    <!-- Photo Library Permissions -->
    <key>NSPhotoLibraryUsageDescription</key>
    <string>SWI Dashboard accesses your photo library to select images for upload. For example, you can choose an existing photo from your library to attach to a report or use as a profile picture.</string>
    
    <key>NSPhotoLibraryAddUsageDescription</key>
    <string>SWI Dashboard saves exported images and reports to your photo library. For example, when you export a report as an image or PDF, the app will save it to your Photos app for easy sharing.</string>
    
    <!-- Microphone Permission -->
    <key>NSMicrophoneUsageDescription</key>
    <string>SWI Dashboard uses your microphone for voice notes and audio recordings. For example, you can record voice notes while inspecting a refrigerator to document observations hands-free, which will be saved as an audio file attached to your report.</string>
</dict>
</plist>
```

## بعد التحديث:

1. **اختبر التطبيق** للتأكد من أن الأذونات تعمل بشكل صحيح
2. **أعد بناء التطبيق** (Clean Build)
3. **أعد رفع التطبيق** إلى App Store Connect
4. **في قسم Review Information**، اذكر أنك قمت بتحديث purpose strings


