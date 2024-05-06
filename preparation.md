# เครื่องมือสำหรับการพัฒนา Flutter

## เตรียมความพร้อม

### การติดตั้ง Homebrew บนระบบปฏิบัติการ Mac

เปิด Application Terminal บน Mac แล้วพิมพ์

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

แล้วระบบจะแนะนำให้เพิ่ม HomeBrew เข้าไปใน path ตัวอย่างเช่น

```
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    (echo; echo 'eval "$(/usr/local/bin/brew shellenv)"') >> /Users/dex/.zprofile
    eval "$(/usr/local/bin/brew shellenv)"
- Run brew help to get started
- Further documentation:
    https://docs.brew.sh
```

โดยเราจะคัดลอกเอา

```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/Bundit/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
```

แล้วกด enter จากนั้นพิมพ์ `source ~/.zprofile` เพื่อทำการเริ่มใช้งาน Homebrew

### การติดตั้ง Winget บนระบบปฏิบัติการ Windows

เปิด Application Command Prompt บน Windows แล้วดาวน์โหลด https://aka.ms/getwinget จากนั้นติดตั้ง Winget

## เครื่องมือสำหรับการพัฒนา Flutter

### 1. Git

[Git](https://git-scm.com) เป็นระบบควบคุมเวอร์ชัน (Version Control System)ที่ใช้สำหรับจัดการและติดตามการเปลี่ยนแปลงของโค้ดในโปรเจ็กต์พัฒนาซอฟต์แวร์ โดย Git ช่วยให้ทีมนักพัฒนาสามารถทำงานร่วมกันได้อย่างมีประสิทธิภาพ ผ่านการแชร์โค้ด ติดตามการแก้ไข และควบคุมเวอร์ชันของโค้ดอย่างเป็นระบบ

### การติดตั้ง Git

Mac (Homebrew)

```bash
brew install git
```

Windows (Winget)

```bash
winget install -e --id Git.Git
```

หรือ [ดาวน์โหลด Git](https://git-scm.com/download/win)

### 2. Android Studio

[Android Studio](https://developer.android.com/studio) เป็น IDE (Integrated Development Environment) ยอดนิยมสำหรับการพัฒนาแอปพลิเคชันบน Android ซึ่งรวมถึงการพัฒนาแอปด้วย Flutter ด้วย โดย Android Studio มีเครื่องมือและปลั๊กอินที่จำเป็นสำหรับการพัฒนา Flutter และช่วยให้นักพัฒนาสามารถเขียนโค้ด ทดสอบ และดีบั๊กแอปพลิเคชัน Flutter ได้อย่างมีประสิทธิภาพ นอกจากนี้ Android Studio ยังมีเอมูเลเตอร์ในตัวสำหรับการรันและทดสอบแอปพลิเคชัน Flutter บนอุปกรณ์ Android เสมือนอีกด้วย

### การติดตั้ง Android Studio

Mac (Homebrew)

```bash
brew install --cask android-studio
```

Windows (Winget)

```bash
winget install -e --id Google.AndroidStudio
```

หรือ [ดาวน์โหลด Android Studio](https://developer.android.com/studio)

### 3. Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) (หรือเรียกสั้นๆ ว่า VS Code) เป็นโปรแกรมแก้ไขโค้ด (Code Editor) ที่ได้รับความนิยมอย่างสูง พัฒนาโดย Microsoft โดย VS Code เป็นโปรแกรมแก้ไขโค้ดแบบ Cross-platform ที่รองรับทั้ง Windows, macOS และ Linux ตัวโปรแกรมมีขนาดเล็ก เร็ว และมีฟีเจอร์ที่หลากหลาย เช่น การเน้นไวยากรณ์ (Syntax Highlighting), อินเทลลิเซนส์โค้ด (IntelliSense), ส่วนขยาย (Extensions) และอื่นๆ อีกมากมาย รวมถึงรองรับการพัฒนาแอปด้วย Flutter ด้วยการติดตั้งส่วนขยาย Dart และ Flutter

### การติดตั้ง Visual Studio Code

Mac (Homebrew)

```bash
brew install --cask visual-studio-code
```

Windows (Winget)

```bash
winget install -e --id Microsoft.VisualStudioCode
```

หรือ [ดาวน์โหลด Visual Studio Code](https://code.visualstudio.com/)

### 4. อื่นๆ

- [Docker](https://www.docker.com/): เป็นแพลตฟอร์มโอเพนซอร์สสำหรับการพัฒนา ส่งมอบ และรันแอปพลิเคชันในรูปแบบของคอนเทนเนอร์

- [Node.js](https://nodejs.org/en/): เป็นรันไทม์ JavaScript ฝั่งเซิร์ฟเวอร์ที่สร้างขึ้นบน Chrome's V8 JavaScript engine ใช้สำหรับพัฒนาแอปพลิเคชันเว็บและเครื่องมือต่างๆ
