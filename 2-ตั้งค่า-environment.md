# **การตั้งค่า Environment**

เพื่อเริ่มพัฒนาด้วย Flutter เราจำเป็นต้องตั้งค่า Environment บนเครื่องคอมพิวเตอร์ ซึ่งรวมถึงการติดตั้งเครื่องมือที่จำเป็นและกำหนดค่าระบบ โดยทำตามขั้นตอนเหล่านี้:

## **การติดตั้ง Flutter SDK**

### 1. การติดตั้ง Flutter SDK บนระบบปฏิบัติการ Windows

### ความต้องการของระบบ

| Requirement                  | Minimum           | Recommended         |
| ---------------------------- | ----------------- | ------------------- |
| x86_64 CPU Cores             | 4                 | 8                   |
| Memory in GB                 | 8                 | 16                  |
| Display resolution in pixels | WXGA (1366 x 768) | FHD (1920 x 1080)   |
| Free disk space in GB        | 11.0              | 60.0                |
| Operating System             | Windows 10        | Windows 10 or later |

### ติดตั้ง Flutter SDK

การดาวน์โหลด Flutter SDK มีหลายวิธี เลือกตัวอย่างใดตัวอย่างหนึ่งดังต่อไปนี้

### วิธีที่ 1. ใช้ VS Code เพื่อติดตั้ง Flutter (แนะนำ)

เพื่อติดตั้ง Flutter โดยใช้คำแนะนำเหล่านี้ ให้ตรวจสอบว่าเราได้ติดตั้ง Visual Studio Code เวอร์ชัน 1.77 หรือใหม่กว่า และส่วนขยาย [Flutter](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) สำหรับ VS Code แล้ว

#### เรียกใช้ VS Code เพื่อติดตั้ง Flutter

1. เปิด VS Code

2. เปิด **Command Palette** โดยกด `Control + Shift + P`

3. ใน **Command Palette** ให้พิมพ์ `flutter`

4. เลือก **Flutter: New Project**

5. VS Code จะแจ้งให้เราระบุตำแหน่งของ Flutter SDK บนคอมพิวเตอร์ของเรา

   1. กรณีที่เราได้ติดตั้ง Flutter SDK ไว้แล้ว ให้คลิก **Locate SDK**

   2. กรณีที่เรายังไม่ได้ติดตั้ง Flutter SDK ให้คลิก **Download SDK**

6. เมื่อได้รับแจ้งว่า **Which Flutter template?** ให้ข้ามไป กด `Esc`

#### ดาวน์โหลด Flutter SDK

1. เมื่อมีข้อความ `Select Folder for Flutter SDK` ปรากฏขึ้น, เลือกตำแหน่งที่เราต้องการให้ Flutter SDK เก็บไว้ในอุปกรณ์ของเรา ให้เลือก `different location` เช่น `%USERPROFILE%` หรือ `C:\Users\username\AppData\Local\flutter` หรือ `C:\dev`

   > \*\* อย่าติดตั้ง Flutter SDK ใน Folder ที่มี
   >
   > - อักขระพิเศษ หรือ เว้นวรรค
   > - Path ที่มีการขอสิทธิ์ในการเข้าถึง
   >
   > ตัวอย่างที่ไม่ควรเก็บไว้เช่น `C:\Program Files\flutter`

2. คลิกที่ปุ่ม `Clone Flutter`

   ในขณะที่ดาวน์โหลด **Flutter**, VS Code จะแสดงการทำงานผ่าน notification :

   ```
   Downloading the Flutter SDK. This may take a few minutes.
   ```

   ระบบจะใช้เวลาสักครู่ หากไม่มีอะไรเกิดขึ้นให้กดปุ่ม `Cancel` และทำรายการใหม่ตั้งแต่ต้นอีกครั้ง

3. เมื่อการดาวน์โหลดเสร็จสิ้นจะได้ Output ดังนี้ :

   ```
   Checking Dart SDK version...
   Downloading Dart SDK from the Flutter engine ...
   Expanding downloaded archive...
   ```

   หากเสร็จสมบูรณ์ ระบบจะแสดงผลบน notification ดังนี้

   ```
   Initializing the Flutter SDK. This may take a few minutes.
   ```

   ระหว่างระบบทำการ initialize ระบบจะใช้เวลาสักครู่ และจะเห็นผลลัพทธ์ดังนี้

   ```
   Building flutter tool...
   Running pub upgrade...
   Resolving dependencies...
   Got dependencies.
   Downloading Material fonts...
   Downloading Gradle Wrapper...
   Downloading package sky_engine...
   Downloading flutter_patched_sdk tools...
   Downloading flutter_patched_sdk_product tools...
   Downloading windows-x64 tools...
   Downloading windows-x64/font-subset tools...
   ```

4. **สำคัญ** เมื่อ Flutter ทำการติดตั้งสำเร็จ ระบบจะถามเราว่าจะให้ติดตั้ง `Flutter SDK` to `PATH` หรือไม่ ? โดยระบบจะแสดงดังนี้

   ```
   Do you want to add the Flutter SDK to PATH so it's accessible
   in external terminals?
   ```

   ให้คลิกเลือกที่ `Add SDK to PATH` เมื่อสำเร็จ ระบบจะแสดงข้อมูลดังนี้

   ```
   The Flutter SDK was added to your PATH
   ```

### วิธีที่ 2. ดาวน์โหลด และ ติดตั้ง

เพื่อจะติดตั้ง `Flutter SDK` ในรูปแบบการดาวน์โหลด เราจะดาวน์โหลด archive (zip) แล้วแตกไฟล์ไฟล์ไปที่เราต้องการ

1. ดาวน์โหลด [Flutter SDK](https://storage.googleapis.com/flutter_infra_release/releases/stable/windows/flutter_windows_3.19.6-stable.zip) ที่เป็น `Stable Version` โดยสามารถเลือก [SDK อื่นๆ](https://docs.flutter.dev/release/archive) ได้เช่นกัน
2. ทำการคลาย zip และคัดลอกไปยัง Folder ที่เราต้องการ เช่น `C:\src\flutter` หรือ `C:\dev\flutter` หรือ `%LOCALAPPDATA%` เช่น (C:\Users\username\AppData\Local\flutter)
   > \*\* อย่าติดตั้ง Flutter SDK ใน Folder ที่มี
   >
   > - อักขระพิเศษ หรือ เว้นวรรค
   > - Path ที่มีการขอสิทธิ์ในการเข้าถึง
   >
   > ตัวอย่างที่ไม่ควรเก็บไว้เช่น `C:\Program Files\flutter`
3. แก้ไข Environment Variable

   - กดปุ่ม start

   - พิมพ์ค้นหาว่า `environments`

   - เลือก `Edit the system environment variables`

   - คลิกที่ปุ่ม `Environment Variables…`

   - ที่กรอบ User variables for <user> คลิกที่ `Path` แล้วเลือกที่ปุ่ม `Edit…`

   - เลือก Browse แล้วเลือก Folder ที่ติดตั้ง Flutter SDK ไว้ เช่น c:\src\flutter\bin

   - กด Ok จนปิดหน้าต่างหมด

### วิธีที่ 3. ติดตั้ง Flutter SDK ด้วยการ Clone จาก GitHub

เป็นวิธีที่ง่ายในการดาวน์โหลด Flutter โดยการ Clone จาก GitHub ไปยัง Folder ที่เราต้องการ

> \*\* เพื่อให้แน่ในว่าจะสามารถติดตั้ง Flutter SDK ในวิธีนี้ได้ โปรดตรวจสอบว่า Git ได้ติดตั้งบนคอมพิวเตอร์แล้วหรือยัง

1. เปิด `Terminal` หรือ `Command Prompt` บน Windows สร้าง Folder โดยพิมพ์
   ```
   git clone https://github.com/flutter/flutter.git -b stable C:\dev\flutter
   ```
   โดยที่ `C:\dev\Flutter` คือตำแหน่งที่เราต้องการให้ Flutter SDK เก็บไว้
2. แก้ไข Environment Variable

   - กดปุ่ม start

   - พิมพ์ค้นหาว่า `environments`

   - เลือก `Edit the system environment variables`

   - คลิกที่ปุ่ม `Environment Variables…`

   - ที่กรอบ User variables for <user> คลิกที่ `Path` แล้วเลือกที่ปุ่ม `Edit…`

   - เลือก Browse แล้วเลือก Folder ที่ติดตั้ง Flutter SDK ไว้ เช่น c:\src\flutter\bin

   - กด Ok จนปิดหน้าต่างหมด

---

### 2. การติดตั้ง Flutter SDK บนระบบปฏิบัติการ MacOS

### ความต้องการของระบบ

| Requirement                  | Minimum              | Recommended                    |
| ---------------------------- | -------------------- | ------------------------------ |
| x86_64 หรือ ARM CPU Cores    | 4                    | 8                              |
| Memory in GB                 | 8                    | 16                             |
| Display resolution in pixels | WXGA (1366 x 768)    | FHD (1920 x 1080)              |
| Free disk space in GB        | 35.0                 | 128.0                          |
| Operating System             | macOS 10.15 Catalina | macOS 12 Monterey หรือใหม่กว่า |

ในบางกรณี Flutter Components บางอันต้องการ Rosetta 2 บน MacOS ที่เป็น `Apple silicon` (M1, M2, M3) เปิด `Terminal`แล้วพิมพ์

```
sudo softwareupdate --install-rosetta --agree-to-license
```

### เครื่องมือในการพัฒนา (จำเป็น)

- [XCode 15](https://developer.apple.com/xcode/) สำหรับการ Debug และ Compile เพื้อให้สามารถทดสอบบน `iOS Simulator` ได้
- [CocoaPods](https://cocoapods.org/) สำหรับ Compile Flutter plugin เพื่อใช้สำหรับ Native app

  ติดตั้ง `CocoaPods` ด้วยคําสั่ง

  ```zsh
  sudo gem install cocoapods
  ```

### ติดตั้ง Flutter SDK

การดาวน์โหลด Flutter SDK มีหลายวิธี เลือกตัวอย่างใดตัวอย่างหนึ่งดังต่อไปนี้

### วิธีที่ 1. ใช้ VS Code เพื่อติดตั้ง Flutter (แนะนำ)

เพื่อติดตั้ง Flutter โดยใช้คำแนะนำเหล่านี้ ให้ตรวจสอบว่าเราได้ติดตั้ง Visual Studio Code เวอร์ชัน 1.77 หรือใหม่กว่า และส่วนขยาย [Flutter](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) สำหรับ VS Code แล้ว

#### เรียกใช้ VS Code เพื่อติดตั้ง Flutter

1. เปิด VS Code

2. เปิด **Command Palette** โดยกด `Command + Shift + P`

3. ใน **Command Palette** ให้พิมพ์ `flutter`

4. เลือก **Flutter: New Project**

5. VS Code จะแจ้งให้เราระบุตำแหน่งของ Flutter SDK บนคอมพิวเตอร์ของเรา

   1. กรณีที่เราได้ติดตั้ง Flutter SDK ไว้แล้ว ให้คลิก **Locate SDK**

   2. กรณีที่เรายังไม่ได้ติดตั้ง Flutter SDK ให้คลิก **Download SDK**

6. เมื่อได้รับแจ้งว่า **Which Flutter template?** ให้ข้ามไป กด `Esc`

#### ดาวน์โหลด Flutter SDK

1. เมื่อมีข้อความ `Select Folder for Flutter SDK` ปรากฏขึ้น, เลือกตำแหน่งที่เราต้องการให้ Flutter SDK เก็บไว้ในอุปกรณ์ของเรา ให้เลือก `different location` เช่น `~/dev` หรือ `/Users/username/dev`

2. คลิกที่ปุ่ม `Clone Flutter`

   ในขณะที่ดาวน์โหลด **Flutter**, VS Code จะแสดงการทำงานผ่าน notification :

   ```
   Downloading the Flutter SDK. This may take a few minutes.
   ```

   ระบบจะใช้เวลาสักครู่ หากไม่มีอะไรเกิดขึ้นให้กดปุ่ม `Cancel` และทำรายการใหม่ตั้งแต่ต้นอีกครั้ง

3. เมื่อการดาวน์โหลดเสร็จสิ้นจะได้ Output ดังนี้ :

   ```
   Checking Dart SDK version...
   Downloading Dart SDK from the Flutter engine ...
   Expanding downloaded archive...
   ```

   หากเสร็จสมบูรณ์ ระบบจะแสดงผลบน notification ดังนี้

   ```
   Initializing the Flutter SDK. This may take a few minutes.
   ```

   ระหว่างระบบทำการ initialize ระบบจะใช้เวลาสักครู่ และจะเห็นผลลัพทธ์ดังนี้

   ```
   Building flutter tool...
   Running pub upgrade...
   Resolving dependencies...
   Got dependencies.
   Downloading Material fonts...
   Downloading Gradle Wrapper...
   Downloading package sky_engine...
   Downloading flutter_patched_sdk tools...
   Downloading flutter_patched_sdk_product tools...
   Downloading windows-x64 tools...
   Downloading windows-x64/font-subset tools...
   ```

4. **สำคัญ** เมื่อ Flutter ทำการติดตั้งสำเร็จ ระบบจะถามเราว่าจะให้ติดตั้ง `Flutter SDK` to `PATH` หรือไม่ ? โดยระบบจะแสดงดังนี้

   ```bash
   Do you want to add the Flutter SDK to PATH so it's accessible
   in external terminals?
   ```

   ให้คลิกเลือกที่ `Add SDK to PATH` เมื่อสำเร็จ ระบบจะแสดงข้อมูลดังนี้

   ```bash
   The Flutter SDK was added to your PATH
   ```

### วิธีที่ 2. ดาวน์โหลด และ ติดตั้ง

เพื่อจะติดตั้ง `Flutter SDK` ในรูปแบบการดาวน์โหลด เราจะดาวน์โหลด archive (zip) แล้วแตกไฟล์ไฟล์ไปที่เราต้องการ

1. ดาวน์โหลด [Flutter SDK (intel Processor)](https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_3.19.6-stable.zip) หรือ [Flutter SDK (Apple Silicon)](https://storage.googleapis.com/flutter_infra_release/releases/stable/macos/flutter_macos_arm64_3.19.6-stable.zip) ที่เป็น `Stable Version` โดยสามารถเลือก [SDK อื่นๆ](https://docs.flutter.dev/release/archive) ได้เช่นกัน
2. สร้าง Folder ไว้ใน `/Users/<username>/development` หรือ `~/development`
3. ทำการคลาย zip และคัดลอกไปยัง Folder ที่เราต้องการ เช่น `~/development` ในรูปแบบ `~/development/flutter`
4. เพิ่ม Flutter ไปยัง `PATH`
   เพื่อรันคำสั่ง Flutter ใน Terminal ให้เพิ่ม Flutter ลงใน environment variable `PATH` คู่มือนี้สันนิษฐานว่า Mac ของเรารันเชลล์เริ่มต้นล่าสุดคือ `zsh` ซึ่ง Zsh จะใช้ไฟล์ `.zshenv` สำหรับตัวแปรสภาพแวดล้อม (environment variables)

   1. เปิด Terminal แล้วพิมพ์

      ```bash
      nano ~/.zshenv
      ```

      หากไม่คุ้นในการใช้ `nano` อาจใช้ `VS Code` ในการเปิดได้เช่นกัน

      ```bash
      code ~/.zshenv
      ```

   2. คัดลอกบรรทัดต่อไปนี้และวางไว้ท้ายสุดของไฟล์ `~/.zshenv`

      ```bash
      export PATH=$HOME/development/flutter/bin:$PATH
      ```

   3. บันทึกไฟล์ `~/.zshenv`

   4. เพื่อให้การเปลี่ยนแปลงนี้มีผล ให้รีสตาร์ทเซสชันของ terminal ทั้งหมดที่เปิดอยู่

### ตั้งค่าเพิ่มเติมสำหรับการพัฒนาบนระบบปฏิบัติการ `iOS`

### กำหนดค่า Xcode

เพื่อพัฒนาแอป Flutter สำหรับ iOS ให้ติดตั้ง Xcode เพื่อคอมไพล์เป็น native bytecode

1. เพื่อกำหนดค่า command-line tools ให้ใช้เวอร์ชันของ Xcode ที่ติดตั้งไว้ ให้รันคำสั่งต่อไปนี้

   ```
   $ sudo sh -c 'xcode-select -s /Applications/Xcode.app/Contents/Developer && xcodebuild -runFirstLaunch'
   ```

   ใช้พาธนี้เพื่อใช้ Xcode เวอร์ชันล่าสุด หากเราต้องการใช้เวอร์ชันอื่น ให้ระบุพาธนั้นแทน

2. ยอมรับข้อตกลงสัญญาอนุญาตของ Xcode

   ```
   $ sudo xcodebuild -license
   ```

พยายามใช้ Xcode เวอร์ชันปัจจุบันให้มากที่สุด
