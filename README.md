تمام يا محمد! خلينا نكمل ونبني شاشة تسجيل الدخول باستخدام Firebase Authentication. الهدف هنا إننا نسمح للمستخدم بالدخول باستخدام البريد الإلكتروني وكلمة المرور.

---

🧩 الخطوة 5: إنشاء شاشة تسجيل الدخول

افتح ملف جديد اسمه login_screen.dart وأضف الكود التالي:

`dart
import 'package:flutter/material.dart';
import 'package:firebaseauth/firebaseauth.dart';

class LoginScreen extends StatefulWidget {
  @override
  LoginScreenState createState() => LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();
  final _auth = FirebaseAuth.instance;

  Future<void> login() async {
    try {
      await _auth.signInWithEmailAndPassword(
        email: _emailController.text.trim(),
        password: _passwordController.text.trim(),
      );
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('تم تسجيل الدخول بنجاح')),
      );
      // انتقل إلى الشاشة الرئيسية بعد تسجيل الدخول
    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('خطأ: ${e.toString()}')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('تسجيل الدخول')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _emailController,
              decoration: InputDecoration(labelText: 'البريد الإلكتروني'),
            ),
            TextField(
              controller: _passwordController,
              decoration: InputDecoration(labelText: 'كلمة المرور'),
              obscureText: true,
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: login,
              child: Text('تسجيل الدخول'),
            ),
          ],
        ),
      ),
    );
  }
}
`

---

🧭 الخطوة 6: ربط الشاشة بـ main.dart

افتح main.dart وعدّل الكود ليعرض شاشة تسجيل الدخول:

`dart
import 'package:flutter/material.dart';
import 'package:firebasecore/firebasecore.dart';
import 'login_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Client Manager',
      home: LoginScreen(),
    );
  }
}
`

---

كده عندنا شاشة تسجيل دخول شغالة! لو المستخدم دخل بيانات صحيحة، يتم تسجيل الدخول.  
الخطوة الجاية: إنشاء شاشة لإضافة العملاء وتخزين بياناتهم في Firestore.

جاهز نكمل؟ 😎
