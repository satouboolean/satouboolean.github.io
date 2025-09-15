# StatefulWidget

The widget class provide state management support

## Main points

- You can receive parameter for the widget when it is called
- Use the received param with `widget.variablename` under State class
- Create state variable under the \_State class
- set the state with `setState(() { statement });` to trigger refresh with state change

## Example

```Dart
class MyWidget extends StatefulWidget {
  const MyWidget({ super.key,required this.requiredParam1, this.optionalParam2 });
  final int requiredParam1;
  final String? optionalParam2;

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  String stateString = '';

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```
