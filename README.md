# flutter_d2_tip_calculator

- main.dart
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final amountController = TextEditingController();
  final discController = TextEditingController();

  List<bool> _selection = [true, false, false];

  String? tip;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              if (tip != null)
                Padding(
                  padding: const EdgeInsets.all(20),
                  child: Text(
                    tip!,
                    style: const TextStyle(fontSize: 30),
                  ),
                ),
              const Text('Total Amount'),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  SizedBox(
                    width: 70,
                    child: TextField(
                      controller: amountController,
                      textAlign: TextAlign.center,
                      decoration: const InputDecoration(hintText: '\$100.00'),
                      keyboardType:
                          const TextInputType.numberWithOptions(decimal: true),
                    ),
                  ),
                  const Padding(padding: EdgeInsets.all(5)),
                  SizedBox(
                    width: 70,
                    child: TextField(
                      controller: discController,
                      textAlign: TextAlign.center,
                      decoration:
                          const InputDecoration(hintText: 'Discon \$100.00'),
                      keyboardType:
                          const TextInputType.numberWithOptions(decimal: true),
                    ),
                  ),
                ],
              ),
              Padding(
                padding: const EdgeInsets.all(20.0),
                child: ToggleButtons(
                  children: const [
                    Text('10%'),
                    Text('15%'),
                    Text('20%'),
                  ],
                  isSelected: _selection,
                  onPressed: updateSelection,
                ),
              ),
              FlatButton(
                onPressed: calculateTip,
                child: const Text('Calculate Tip'),
                color: Colors.green,
                textColor: Colors.white,
              )
            ],
          ),
        ),
      ),
    );
  }

  void updateSelection(int selectedIndex) {
    setState(() {
      for (int i = 0; i < _selection.length; i++) {
        _selection[i] = selectedIndex == i;
      }
    });
  }

  void calculateTip() {
    final totalAmount = double.parse(amountController.text);
    final selectedIndex = _selection.indexWhere((element) => element);
    final tipPersentage = [0.1, 0.15, 0.2][selectedIndex];

    final tipTotal = (totalAmount * tipPersentage).toStringAsFixed(2);
    final disc = (totalAmount + totalAmount * tipPersentage).toStringAsFixed(2);

    setState(() {
      tip = '\$$tipTotal';
      discController.text = '\$$disc';
    });
  }
}
```

---

```
Copyright 2022 M. Fadli Zein
```