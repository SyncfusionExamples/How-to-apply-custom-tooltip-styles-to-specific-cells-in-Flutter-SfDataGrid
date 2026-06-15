# How-to-apply-custom-tooltip-styles-to-specific-cells-in-Flutter-SfDataGrid

In this article, we will show how to apply custom tooltip styles to specific cells in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the required configurations. In the default implementation, cells are rendered using basic widgets without any additional interaction or visual enhancements.

To display contextual information for each cell, you can wrap the widget inside the `DataGridCell` with a [Tooltip](https://api.flutter.dev/flutter/material/Tooltip-class.html) widget within the [DataGridSource.buildRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/buildRow.html) method. By assigning the cell value to the [Tooltip.message](https://api.flutter.dev/flutter/material/Tooltip/message.html) property, the corresponding content will be displayed when the user hovers over the cell.

To customize the appearance of the tooltip, you can define a [BoxDecoration](https://api.flutter.dev/flutter/painting/BoxDecoration-class.html) and assign it to the [Tooltip.decoration](https://api.flutter.dev/flutter/material/Tooltip/decoration.html) property. Using the [BoxDecoration.color](https://api.flutter.dev/flutter/painting/BoxDecoration/color.html), you can set the desired background color for the tooltip, enabling a more visually distinct and user-friendly presentation.

```dart
  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    return DataGridRowAdapter(
      cells: row.getCells().map<Widget>((e) {
        // Properties to check the column name and value to set different background colors for tooltip
        bool isDesignationColumn = e.columnName == 'designation';
        bool isNameColumn = e.columnName == 'name';
        bool isSalaryColumn = e.columnName == 'salary';
        bool isHighSalary = isSalaryColumn && (e.value as int) >= 20000;

        // Return a tooltip with different background colors based on the conditions
        return Tooltip(
          message: e.value.toString(), // Show the value in the tooltip
          decoration: BoxDecoration(
            // Set background color based on the column and value
            color: isHighSalary
                ? Colors.yellow
                : isSalaryColumn
                ? Colors.green
                : isDesignationColumn
                ? Colors.red
                : isNameColumn
                ? Colors.blue
                : Colors.grey,
            borderRadius: BorderRadius.circular(4.0),
          ),
          child: Container(
            alignment: Alignment.center,
            padding: EdgeInsets.all(8.0),
            child: Text(e.value.toString()),
          ),
        );
      }).toList(),
    );
  }

```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-apply-custom-tooltip-styles-to-specific-cells-in-Flutter-SfDataGrid).
