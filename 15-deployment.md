# Deployment

## Android

เมื่อเราพร้อมที่จะเตรียมเวอร์ชัน release ของแอป เช่น เพื่อ[เผยแพร่ไปยัง Google Play Store][play] หน้านี้สามารถช่วยเราได้ ก่อนการเผยแพร่ เราอาจต้องการเพิ่มรายละเอียดสุดท้ายให้กับแอป คู่มือนี้จะอธิบายวิธีการทำงานต่อไปนี้:

## เพิ่มไอคอนตัวเปิดใช้งาน

เมื่อสร้างแอป Flutter ใหม่ มันจะมีไอคอนตัวเปิดใช้งานเริ่มต้น หากเราต้องการปรับแต่งไอคอนนี้ เราอาจต้องการดูแพ็คเกจ [flutter_launcher_icons][] หรือเราสามารถทำด้วยตนเองโดยใช้ขั้นตอนต่อไปนี้:

1. ตรวจสอบแนวทาง [Material Design product icons](https://github.com/flutter/website/blob/main/src/content/deployment/%7B%7Bsite.material%7D%7D/styles/icons) สำหรับการออกแบบไอคอน
2. ในไดเรกทอรี `[project]/android/app/src/main/res/` วางไฟล์ไอคอนของเราในโฟลเดอร์ที่ตั้งชื่อโดยใช้ [configuration qualifiers](https://github.com/flutter/website/blob/main/src/content/deployment/%7B%7Bsite.android-dev%7D%7D/guide/topics/resources/providing-resources#AlternativeResources) โฟลเดอร์ `mipmap-` เริ่มต้นแสดงให้เห็นการตั้งชื่ออย่างถูกต้อง
3. ใน `AndroidManifest.xml` ให้อัปเดตแอตทริบิวต์ `android:icon` ของแท็ก [`application`](https://github.com/flutter/website/blob/main/src/content/deployment/%7B%7Bsite.android-dev%7D%7D/guide/topics/manifest/application-element) เพื่ออ้างอิงไอคอนจากขั้นตอนก่อนหน้า (เช่น `<application android:icon="@mipmap/ic_launcher" ...>`)
4. เพื่อตรวจสอบว่าไอคอนถูกแทนที่แล้ว ให้เรารันแอปและตรวจสอบไอคอนแอปใน Launcher

## เปิดใช้งาน Material Components

หากแอปของเราใช้ [Platform Views](https://github.com/flutter/website/blob/main/platform-integration/android/platform-views) เราอาจต้องการเปิดใช้งาน Material Components โดยทำตามขั้นตอนที่อธิบายไว้ใน [Getting Started guide for Android][] ตัวอย่างเช่น:

1. เพิ่ม dependency ของ Android's Material ใน `<my-app>/android/app/build.gradle`:

```groovy
dependencies {
    // ...
    implementation 'com.google.android.material:material:<version>'
    // ...
}
```

เพื่อดูเวอร์ชันล่าสุด ให้ไปที่ [Google Maven](https://maven.google.com/web/index.html#com.google.android.material:material)

2. ตั้งค่าธีมสว่างใน `<my-app>/android/app/src/main/res/values/styles.xml`:

```diff
-<style name="NormalTheme" parent="@android:style/Theme.Light.NoTitleBar">
+<style name="NormalTheme" parent="Theme.MaterialComponents.Light.NoActionBar">
```

3. ตั้งค่าธีมมืดใน `<my-app>/android/app/src/main/res/values-night/styles.xml`

```diff
-<style name="NormalTheme" parent="@android:style/Theme.Black.NoTitleBar">
+<style name="NormalTheme" parent="Theme.MaterialComponents.DayNight.NoActionBar">
```

## ลงชื่อแอป

เพื่อเผยแพร่บน Play Store เราจำเป็นต้องลงชื่อแอปของเราด้วยใบรับรองดิจิทัล Android ใช้คีย์ลงชื่อสองแบบ: _upload_ และ _app signing_

- นักพัฒนาอัปโหลดไฟล์ `.aab` หรือ `.apk` ที่ลงชื่อด้วย _upload key_ ไปยัง Play Store
- ผู้ใช้ปลายทางดาวน์โหลดไฟล์ `.apk` ที่ลงชื่อด้วย _app signing key_

เพื่อสร้าง app signing key ของเรา ให้ใช้ Play App Signing ตามที่อธิบายไว้ใน [เอกสารทางการของ Play Store][]

เพื่อลงชื่อแอปของเรา ให้ใช้คำแนะนำต่อไปนี้

### สร้าง upload keystore

หากเรามี keystore อยู่แล้ว ให้ข้ามไปยังขั้นตอนถัดไป หากไม่มี ให้สร้างอันใหม่โดยใช้วิธีใดวิธีหนึ่งต่อไปนี้:

1. ทำตาม[ขั้นตอนการสร้างคีย์ของ Android Studio]({{site.android-dev}}/studio/publish/app-signing#generate-key)

2. รันคำสั่งต่อไปนี้ที่บรรทัดคำสั่ง:

   บน macOS หรือ Linux ให้ใช้คำสั่งต่อไปนี้:

   ```console
   keytool -genkey -v -keystore ~/upload-keystore.jks -keyalg RSA \
   -keysize 2048 -validity 10000 -alias upload
   ```

   บน Windows ให้ใช้คำสั่งต่อไปนี้ใน PowerShell:

   ```powershell
   keytool -genkey -v -keystore %userprofile%\upload-keystore.jks ^
   -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 ^
   -alias upload
   ```

   คำสั่งนี้จะจัดเก็บไฟล์ `upload-keystore.jks` ในไดเรกทอรีหลักของเรา หากเราต้องการจัดเก็บไว้ที่อื่น ให้เปลี่ยนอาร์กิวเมนต์ที่เราส่งให้พารามิเตอร์ `-keystore`

   **อย่างไรก็ตาม ให้รักษาไฟล์ `keystore` ไว้เป็นส่วนตัว อย่าเช็คอินเข้าไปในการควบคุมซอร์สโค้ดสาธารณะ!**

### อ้างอิง keystore จากแอป

สร้างไฟล์ชื่อ `[project]/android/key.properties` ที่มีการอ้างอิงถึง keystore ของเรา อย่ารวมเครื่องหมายเปิดปิดมุม (`< >`) เข้าไป มันบ่งบอกว่าข้อความนั้นทำหน้าที่เป็นตัวยึดตำแหน่งสำหรับค่าของเรา

```properties
storePassword=<password-from-previous-step>
keyPassword=<password-from-previous-step>
keyAlias=upload
storeFile=<keystore-file-location>
```

`storeFile` อาจอยู่ที่ `/Users/<user name>/upload-keystore.jks` บน macOS หรือ `C:\\Users\\<user name>\\upload-keystore.jks` บน Windows

### กำหนดค่าการลงชื่อใน gradle

เมื่อสร้างแอปของเราในโหมด release ให้กำหนดค่า gradle ให้ใช้ upload key ของเรา เพื่อกำหนดค่า gradle ให้แก้ไขไฟล์ `<project>/android/app/build.gradle`

1. เพิ่มข้อมูล keystore จากไฟล์ properties ของเราก่อนบล็อก `android`:

   ```diff
   + def keystoreProperties = new Properties()
   + def keystorePropertiesFile = rootProject.file('key.properties')
   + if (keystorePropertiesFile.exists()) {
   +     keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
   + }
   +
   android {
       ...
   }
   ```

2. โหลดไฟล์ `key.properties` เข้าไปในออบเจกต์ `keystoreProperties`

3. เพิ่มการกำหนดค่าการลงชื่อก่อนบล็อก `buildTypes`:

   ```diff
   +    signingConfigs {
   +        release {
   +            keyAlias keystoreProperties['keyAlias']
   +            keyPassword keystoreProperties['keyPassword']
   +            storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
   +            storePassword keystoreProperties['storePassword']
   +        }
   +    }
        buildTypes {
            release {
                // TODO: Add your own signing config for the release build.
                // Signing with the debug keys for now,
                // so `flutter run --release` works.
   -            signingConfig signingConfigs.debug
   +            signingConfig signingConfigs.release
            }
        }
   ```

## สร้างแอปสำหรับ release

เรามีรูปแบบ release ที่เป็นไปได้สองแบบเมื่อเผยแพร่ไปยัง Play Store

- App bundle (แนะนำ)
- APK

### สร้าง app bundle

ส่วนนี้จะอธิบายวิธีสร้าง release app bundle หากเราทำขั้นตอนการลงชื่อเสร็จสมบูรณ์ app bundle จะถูกลงชื่อ ณ จุดนี้ เราอาจพิจารณา[การทำโค้ด Dart ของเราให้ยากต่อการเข้าใจ][] เพื่อให้ยากต่อการทำวิศวกรรมย้อนกลับ การทำโค้ดของเราให้ยากต่อการเข้าใจนั้นเกี่ยวข้องกับการเพิ่มแฟล็กสองสามตัวในคำสั่ง build และการดูแลไฟล์เพิ่มเติมเพื่อแก้ stack traces

จากบรรทัดคำสั่ง:

1. ป้อน `cd [project]`<br>
2. รัน `flutter build appbundle`<br>
   (การรัน `flutter build` จะเป็นการ build แบบ release โดยค่าเริ่มต้น)

release bundle สำหรับแอปของเราจะถูกสร้างขึ้นที่ `[project]/build/app/outputs/bundle/release/app.aab`

โดยค่าเริ่มต้น app bundle จะมีโค้ด Dart ของเราและ Flutter runtime ที่คอมไพล์สำหรับ [armeabi-v7a][] (ARM 32-bit), [arm64-v8a][] (ARM 64-bit), และ [x86-64][] (x86 64-bit)

### สร้าง APK

แม้ว่า app bundle จะเป็นที่นิยมมากกว่า APK แต่ก็ยังมีร้านค้าบางแห่งที่ไม่รองรับ app bundle ในกรณีนี้ ให้สร้าง release APK สำหรับ ABI (Application Binary Interface) เป้าหมายแต่ละตัว หากเราทำขั้นตอนการลงชื่อเสร็จสมบูรณ์ APK จะถูกลงชื่อ ณ จุดนี้ เราอาจพิจารณา[การทำโค้ด Dart ของเราให้ยากต่อการเข้าใจ][] เพื่อให้ยากต่อการทำวิศวกรรมย้อนกลับ การทำโค้ดของเราให้ยากต่อการเข้าใจนั้นเกี่ยวข้องกับการเพิ่มแฟล็กสองสามตัวในคำสั่ง build

จากบรรทัดคำสั่ง:

1. ป้อน `cd [project]`
2. รัน `flutter build apk --split-per-abi` (คำสั่ง `flutter build` จะเป็น `--release` โดยค่าเริ่มต้น)

คำสั่งนี้จะสร้างไฟล์ APK สามไฟล์:

- `[project]/build/app/outputs/apk/release/app-armeabi-v7a-release.apk`
- `[project]/build/app/outputs/apk/release/app-arm64-v8a-release.apk`
- `[project]/build/app/outputs/apk/release/app-x86_64-release.apk`

การลบแฟล็ก `--split-per-abi` จะทำให้ได้ fat APK ที่มีโค้ดของเราที่คอมไพล์สำหรับ ABI เป้าหมาย*ทั้งหมด* APK ดังกล่าวจะมีขนาดใหญ่กว่า APK ที่แยกกัน ทำให้ผู้ใช้ต้องดาวน์โหลดไบนารีดั้งเดิมที่ไม่เกี่ยวข้องกับสถาปัตยกรรมของอุปกรณ์

### ติดตั้ง APK บนอุปกรณ์

ทำตามขั้นตอนเหล่านี้เพื่อติดตั้ง APK บนอุปกรณ์ Android ที่เชื่อมต่อ

จากบรรทัดคำสั่ง:

1. เชื่อมต่ออุปกรณ์ Android ของเรากับคอมพิวเตอร์ด้วยสาย USB
2. ป้อน `cd [project]`
3. รัน `flutter install`

## เผยแพร่ไปยัง Google Play Store

สำหรับคำแนะนำโดยละเอียดเกี่ยวกับการเผยแพร่แอปของเราไปยัง Google Play Store โปรดดู[เอกสารการเปิดตัว Google Play][play]

## อัปเดตหมายเลขเวอร์ชันของแอป

หมายเลขเวอร์ชันเริ่มต้นของแอปคือ `1.0.0` เพื่ออัปเดตมัน ให้ไปที่ไฟล์ `pubspec.yaml` และอัปเดตบรรทัดต่อไปนี้:

```yaml
version: 1.0.0+1
```

หมายเลขเวอร์ชันคือตัวเลขสามตัวที่คั่นด้วยจุด เช่น `1.0.0` ในตัวอย่างข้างต้น ตามด้วยหมายเลขบิลด์เสริม เช่น `1` ในตัวอย่างข้างต้น คั่นด้วย `+` ทั้งเวอร์ชันและหมายเลขบิลด์สามารถถูกเขียนทับใน build ของ Flutter ได้โดยระบุ `--build-name` และ `--build-number` ตามลำดับ

ใน Android `build-name` จะถูกใช้เป็น `versionName` ขณะที่ `build-number` ใช้เป็น `versionCode` สำหรับข้อมูลเพิ่มเติม โปรดดู[เวอร์ชันแอปของคุณ][] ในเอกสารของ Android

เมื่อเราสร้างแอปสำหรับ Android ใหม่ การอัปเดตหมายเลขเวอร์ชันใดๆ จากไฟล์ pubspec จะอัปเดต `versionName` และ `versionCode` ในไฟล์ `local.properties`
