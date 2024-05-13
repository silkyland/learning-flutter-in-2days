# ทดลองทำ Layout ด้วย Flutter

1. จงสร้าง User Interface ใน Flutter ประกอบด้วยกล่องสีต่างๆ ดังนี้

   ![Practice Layout](/assets/images/practice/practice_layout.png)

   1. กล่องสีแดง ขนาดกว้าง 100 สูง 100 พิกเซล
   2. กล่องสีเขียว ขนาดกว้าง 150 สูง 100 พิกเซล
   3. กล่องสีน้ำเงิน ขนาดกว้าง 100 สูง 150 พิกเซล
   4. จัดวางกล่องทั้ง 3 กล่องให้เรียงกันในแนวนอน โดยให้อยู่กึ่งกลางของหน้าจอ

   <details>
   <summary>เฉลย: (พยายามทำด้วยตัวเองก่อนอย่าพึ่งเปิดเฉลยนะครับ) </summary>

   ```dart
   import 'package:flutter/material.dart';

   void main() {
   runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
   @override
   Widget build(BuildContext context) {
       return MaterialApp(
       home: Scaffold(
           body: Center(
           child: Row(
               mainAxisAlignment: MainAxisAlignment.center,
               children: [
               Container(
                   width: 100,
                   height: 100,
                   color: Colors.red,
               ),
               SizedBox(width: 10),
               Container(
                   width: 150,
                   height: 100,
                   color: Colors.green,
               ),
               SizedBox(width: 10),
               Container(
                   width: 100,
                   height: 150,
                   color: Colors.blue,
               ),
               ],
           ),
           ),
       ),
       );
   }
   }
   ```

   คำอธิบาย:

   1. เราสร้าง `Container` สำหรับกล่องสีแดง ขนาดกว้าง 100 สูง 100 พิกเซล โดยใช้ `color: Colors.red`
   2. เราสร้าง `Container` สำหรับกล่องสีเขียว ขนาดกว้าง 150 สูง 100 พิกเซล โดยใช้ `color: Colors.green`
   3. เราสร้าง `Container` สำหรับกล่องสีน้ำเงิน ขนาดกว้าง 100 สูง 150 พิกเซล โดยใช้ `color: Colors.blue`
   4. เราใช้ `Row` เพื่อจัดวางกล่องทั้ง 3 กล่องในแนวนอน โดยใช้ `mainAxisAlignment: MainAxisAlignment.center` เพื่อให้อยู่กึ่งกลางของแนวนอน
   5. เราใช้ `SizedBox` เพื่อสร้างช่องว่างระหว่างกล่อง ในที่นี้กำหนดความกว้าง 10 พิกเซล
   6. สุดท้ายเราครอบทั้งหมดไว้ใน `Center` เพื่อให้อยู่กึ่งกลางของหน้าจอ

   </details>

---

2. จงสร้าง User Interface ใน Flutter ประกอบด้วยกล่องสีต่างๆ ดังนี้

   ![Practice Layout](/assets/images/practice/layoutmix.png)

   1. กล่องสีแดง ขนาดกว้าง 100 สูง 100 พิกเซล
   2. กล่องสีเขียว ขนาดกว้าง 150 สูง 80 พิกเซล
   3. กล่องสีน้ำเงิน ขนาดกว้าง 120 สูง 120 พิกเซล
   4. กล่องสีส้ม ขนาดกว้าง 80 สูง 150 พิกเซล
   5. จัดวางกล่องสีแดงและสีเขียวให้อยู่ในแนวนอน ส่วนกล่องสีน้ำเงินและสีส้มให้อยู่ในแนวตั้ง
   6. จัดวางกลุ่มกล่องแนวนอนและแนวตั้งให้อยู่กึ่งกลางของหน้าจอ

   <details>
    <summary>เฉลย: (พยายามทำด้วยตัวเองก่อนอย่าพึ่งเปิดเฉลยนะครับ) </summary>

   ```dart
   import 'package:flutter/material.dart';

   void main() {
   runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
   @override
   Widget build(BuildContext context) {
       return MaterialApp(
       home: Scaffold(
           body: Center(
           child: Row(
               mainAxisAlignment: MainAxisAlignment.center,
               children: [
               Column(
                   mainAxisAlignment: MainAxisAlignment.center,
                   children: [
                   Container(
                       width: 100,
                       height: 100,
                       color: Colors.red,
                   ),
                   SizedBox(height: 10),
                   Container(
                       width: 150,
                       height: 80,
                       color: Colors.green,
                   ),
                   ],
               ),
               SizedBox(width: 20),
               Column(
                   mainAxisAlignment: MainAxisAlignment.center,
                   children: [
                   Container(
                       width: 120,
                       height: 120,
                       color: Colors.blue,
                   ),
                   SizedBox(height: 10),
                   Container(
                       width: 80,
                       height: 150,
                       color: Colors.orange,
                   ),
                   ],
               ),
               ],
           ),
           ),
       ),
       );
   }
   }
   ```

   คำอธิบาย:

   1. เราสร้าง `Container` สำหรับกล่องสีต่างๆ ตามขนาดที่กำหนด โดยใช้ `color` เพื่อกำหนดสี
   2. เราใช้ `Column` เพื่อจัดวางกล่องสีแดงและสีเขียวในแนวตั้ง โดยใช้ `mainAxisAlignment: MainAxisAlignment.center` เพื่อให้อยู่กึ่งกลางของแนวตั้ง
   3. เราใช้ `Column` เพื่อจัดวางกล่องสีน้ำเงินและสีส้มในแนวตั้ง โดยใช้ `mainAxisAlignment: MainAxisAlignment.center` เพื่อให้อยู่กึ่งกลางของแนวตั้ง
   4. เราใช้ `Row` เพื่อจัดวางกลุ่มกล่องแนวตั้งทั้งสองกลุ่มในแนวนอน โดยใช้ `mainAxisAlignment: MainAxisAlignment.center` เพื่อให้อยู่กึ่งกลางของแนวนอน
   5. เราใช้ `SizedBox` เพื่อสร้างช่องว่างระหว่างกล่องและระหว่างกลุ่มกล่อง
   6. สุดท้ายเราครอบทั้งหมดไว้ใน `Center` เพื่อให้อยู่กึ่งกลางของหน้าจอ

   </details>
