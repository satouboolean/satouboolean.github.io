# StatelessWidget

The widget class without state support

## Main points

- You can receive parameter for the widget when it is called

## Example

```Dart
class MyWidget extends StatefulWidget {
  const MyWidget({ super.key,required this.requiredParam1, this.optionalParam2 });
  final int requiredParam1;
  final String? optionalParam2;

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```
