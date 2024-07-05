

# แบบฝึกหัด: พัฒนาแอปบันทึกรายรับรายจ่ายด้วย Flutter และ Firebase

![Expense Tracker](/assets/firebase/expense.svg)

## โจทย์ 1: การตั้งค่า Firebase
สร้างโปรเจค Flutter ใหม่และตั้งค่า Firebase สำหรับโปรเจคของคุณ

**เฉลย:**
1. สร้างโปรเจค Flutter: `flutter create income_expense_app`
2. เพิ่ม dependencies ใน pubspec.yaml:
   ```yaml
   dependencies:
     firebase_core: ^2.13.1
     firebase_auth: ^4.6.2
     cloud_firestore: ^4.8.0
   ```
3. ตั้งค่า Firebase ในโปรเจค (ใช้ FlutterFire CLI หรือทำด้วยตนเอง)
4. เพิ่มโค้ดเริ่มต้น Firebase ใน main.dart:
   ```dart
   void main() async {
     WidgetsFlutterBinding.ensureInitialized();
     await Firebase.initializeApp();
     runApp(MyApp());
   }
   ```

## โจทย์ 2: การสร้างหน้าเพิ่มรายการ
สร้างหน้าสำหรับเพิ่มรายการรายรับหรือรายจ่ายใหม่

**เฉลย:**
```dart
class AddTransactionPage extends StatefulWidget {
  @override
  _AddTransactionPageState createState() => _AddTransactionPageState();
}

class _AddTransactionPageState extends State<AddTransactionPage> {
  final _formKey = GlobalKey<FormState>();
  String _type = 'income';
  String _description = '';
  double _amount = 0;

  void _submitForm() {
    if (_formKey.currentState!.validate()) {
      _formKey.currentState!.save();
      FirebaseFirestore.instance.collection('transactions').add({
        'type': _type,
        'description': _description,
        'amount': _amount,
        'date': Timestamp.now(),
        'userId': FirebaseAuth.instance.currentUser!.uid,
      });
      Navigator.pop(context);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('เพิ่มรายการใหม่')),
      body: Form(
        key: _formKey,
        child: ListView(
          padding: EdgeInsets.all(16.0),
          children: [
            DropdownButtonFormField<String>(
              value: _type,
              items: ['income', 'expense'].map((String value) {
                return DropdownMenuItem<String>(
                  value: value,
                  child: Text(value == 'income' ? 'รายรับ' : 'รายจ่าย'),
                );
              }).toList(),
              onChanged: (String? newValue) {
                setState(() {
                  _type = newValue!;
                });
              },
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'คำอธิบาย'),
              onSaved: (value) => _description = value!,
              validator: (value) => value!.isEmpty ? 'กรุณากรอกคำอธิบาย' : null,
            ),
            TextFormField(
              decoration: InputDecoration(labelText: 'จำนวนเงิน'),
              keyboardType: TextInputType.number,
              onSaved: (value) => _amount = double.parse(value!),
              validator: (value) => value!.isEmpty ? 'กรุณากรอกจำนวนเงิน' : null,
            ),
            ElevatedButton(
              child: Text('บันทึก'),
              onPressed: _submitForm,
            ),
          ],
        ),
      ),
    );
  }
}
```

## โจทย์ 3: การแสดงรายการธุรกรรม
สร้างหน้าหลักที่แสดงรายการธุรกรรมทั้งหมดของผู้ใช้

**เฉลย:**
```dart
class TransactionListPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('รายการธุรกรรม')),
      body: StreamBuilder<QuerySnapshot>(
        stream: FirebaseFirestore.instance
            .collection('transactions')
            .where('userId', isEqualTo: FirebaseAuth.instance.currentUser!.uid)
            .orderBy('date', descending: true)
            .snapshots(),
        builder: (context, snapshot) {
          if (!snapshot.hasData) return CircularProgressIndicator();
          return ListView(
            children: snapshot.data!.docs.map((doc) {
              Map<String, dynamic> data = doc.data() as Map<String, dynamic>;
              return ListTile(
                title: Text(data['description']),
                subtitle: Text('${data['type'] == 'income' ? '+' : '-'}${data['amount']} บาท'),
                trailing: Text(data['date'].toDate().toString().split(' ')[0]),
              );
            }).toList(),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        child: Icon(Icons.add),
        onPressed: () => Navigator.push(
          context,
          MaterialPageRoute(builder: (_) => AddTransactionPage()),
        ),
      ),
    );
  }
}
```

## โจทย์ 4: การคำนวณยอดคงเหลือ
เพิ่มการแสดงยอดคงเหลือที่คำนวณจากรายรับและรายจ่ายทั้งหมด

**เฉลย:**
```dart
class BalanceWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StreamBuilder<QuerySnapshot>(
      stream: FirebaseFirestore.instance
          .collection('transactions')
          .where('userId', isEqualTo: FirebaseAuth.instance.currentUser!.uid)
          .snapshots(),
      builder: (context, snapshot) {
        if (!snapshot.hasData) return CircularProgressIndicator();
        
        double balance = 0;
        snapshot.data!.docs.forEach((doc) {
          Map<String, dynamic> data = doc.data() as Map<String, dynamic>;
          if (data['type'] == 'income') {
            balance += data['amount'];
          } else {
            balance -= data['amount'];
          }
        });
        
        return Card(
          child: Padding(
            padding: EdgeInsets.all(16.0),
            child: Text(
              'ยอดคงเหลือ: ${balance.toStringAsFixed(2)} บาท',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
          ),
        );
      },
    );
  }
}
```

## โจทย์ 5: การเพิ่มการกรองและการค้นหา
เพิ่มฟีเจอร์การกรองรายการตามประเภท (รายรับ/รายจ่าย) และการค้นหาตามคำอธิบาย

**เฉลย:**
```dart
class FilteredTransactionList extends StatefulWidget {
  @override
  _FilteredTransactionListState createState() => _FilteredTransactionListState();
}

class _FilteredTransactionListState extends State<FilteredTransactionList> {
  String _filterType = 'all';
  String _searchQuery = '';

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Row(
          children: [
            DropdownButton<String>(
              value: _filterType,
              items: ['all', 'income', 'expense'].map((String value) {
                return DropdownMenuItem<String>(
                  value: value,
                  child: Text(value == 'all' ? 'ทั้งหมด' : (value == 'income' ? 'รายรับ' : 'รายจ่าย')),
                );
              }).toList(),
              onChanged: (String? newValue) {
                setState(() {
                  _filterType = newValue!;
                });
              },
            ),
            Expanded(
              child: TextField(
                decoration: InputDecoration(labelText: 'ค้นหา'),
                onChanged: (value) {
                  setState(() {
                    _searchQuery = value;
                  });
                },
              ),
            ),
          ],
        ),
        Expanded(
          child: StreamBuilder<QuerySnapshot>(
            stream: FirebaseFirestore.instance
                .collection('transactions')
                .where('userId', isEqualTo: FirebaseAuth.instance.currentUser!.uid)
                .snapshots(),
            builder: (context, snapshot) {
              if (!snapshot.hasData) return CircularProgressIndicator();
              
              var filteredDocs = snapshot.data!.docs.where((doc) {
                Map<String, dynamic> data = doc.data() as Map<String, dynamic>;
                bool matchesType = _filterType == 'all' || data['type'] == _filterType;
                bool matchesSearch = _searchQuery.isEmpty ||
                    data['description'].toLowerCase().contains(_searchQuery.toLowerCase());
                return matchesType && matchesSearch;
              }).toList();
              
              return ListView(
                children: filteredDocs.map((doc) {
                  Map<String, dynamic> data = doc.data() as Map<String, dynamic>;
                  return ListTile(
                    title: Text(data['description']),
                    subtitle: Text('${data['type'] == 'income' ? '+' : '-'}${data['amount']} บาท'),
                    trailing: Text(data['date'].toDate().toString().split(' ')[0]),
                  );
                }).toList(),
              );
            },
          ),
        ),
      ],
    );
  }
}
```

ทั้ง 5 โจทย์นี้ครอบคลุมฟีเจอร์หลักของแอปบันทึกรายรับรายจ่าย ซึ่งรวมถึงการเพิ่มรายการใหม่ การแสดงรายการทั้งหมด การคำนวณยอดคงเหลือ และการกรอง/ค้นหารายการ คุณสามารถนำโค้ดเหล่านี้ไปปรับใช้และต่อยอดเพื่อพัฒนาแอปให้สมบูรณ์ยิ่งขึ้นได้