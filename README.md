# flex_table

A highly customizable Flutter table widget built on top of Flutter's native
`Table`. It covers the common table patterns you reach for in data-heavy apps —
without locking you into a rigid design.

## Features

- **Flexible column widths** — `FlexColumnWidth`, `FixedColumnWidth`,
  `IntrinsicColumnWidth`, `FractionColumnWidth`, or mix `minWidth`/`maxWidth`
  constraints
- **Sortable columns** — built-in ascending/descending arrow icons,
  `onSort` callback
- **Row selection** — leading checkbox column, select-all tristate, custom
  checkbox builder
- **Expandable rows** — tap an indicator to reveal arbitrary content below a row
- **Collapsible groups** — named sections that users can collapse to hide rows
- **Column visibility** — hide/show columns at runtime with `visible: false`
- **Striped / alternating rows** — `FlexTableTheme.striped(context)`
- **Footer rows** — for totals, averages, or any summary data
- **Loading & empty states** — sensible defaults with custom builder overrides
- **Hover effects** — mouse-region highlighting (disable for touch-only targets)
- **Row & cell interactions** — `onRowTap`, `onRowDoubleTap`, `onRowLongPress`,
  `onRowSecondaryTap`, `onCellTap`
- **Per-row dividers** — `rowDivider: BorderSide(...)` paints a full-width line
  between rows
- **Column tooltips** — `FlexTableColumn(tooltip: 'hint')`
- **Row tooltips** — `FlexTableRow(tooltip: 'hint')`
- **Comprehensive theming** — override every decoration, padding, alignment, and
  text style via `FlexTableTheme` and its `copyWith`
- **`copyWith` everywhere** — `FlexTableColumn`, `FlexTableRow`,
  `FlexTableGroup`, and `FlexTableTheme` all support immutable updates

## Getting started

Add the dependency to your `pubspec.yaml`:

```yaml
dependencies:
  flex_table: ^0.1.0
```

Then import it:

```dart
import 'package:flex_table/flex_table.dart';
```

## Usage

### Basic table

```dart
FlexTable(
  columns: [
    FlexTableColumn(header: Text('Name'), width: FlexColumnWidth(2)),
    FlexTableColumn(header: Text('Age'),  width: FixedColumnWidth(80)),
    FlexTableColumn(header: Text('City'), width: FlexColumnWidth(1)),
  ],
  rows: [
    FlexTableRow(cells: [Text('Alice'), Text('28'), Text('New York')]),
    FlexTableRow(cells: [Text('Bob'),   Text('34'), Text('Berlin')]),
  ],
)
```

### Sortable columns

```dart
FlexTable(
  sortColumnIndex: _sortIndex,
  sortAscending: _ascending,
  onSort: (index) {
    setState(() {
      if (_sortIndex == index) {
        _ascending = !_ascending;
      } else {
        _sortIndex = index;
        _ascending = true;
      }
      // sort your data list here
    });
  },
  columns: [
    FlexTableColumn(header: Text('Name'), sortable: true),
    FlexTableColumn(header: Text('Age'),  sortable: true),
  ],
  rows: _people.map((p) =>
    FlexTableRow(cells: [Text(p.name), Text('${p.age}')])).toList(),
)
```

### Row selection with checkboxes

```dart
FlexTable(
  showCheckboxes: true,
  selectedRows: _selected,
  onRowSelected: (index) => setState(() {
    _selected.contains(index)
        ? _selected.remove(index)
        : _selected.add(index);
  }),
  onSelectAll: (value) => setState(() {
    _selected = value == true
        ? Set.from(List.generate(_rows.length, (i) => i))
        : {};
  }),
  columns: [ /* ... */ ],
  rows: _rows,
)
```

### Expandable rows

```dart
FlexTable(
  expandedRows: _expanded,
  onRowExpanded: (index) => setState(() {
    _expanded.contains(index)
        ? _expanded.remove(index)
        : _expanded.add(index);
  }),
  expandableRowBuilder: (context, row, index) => Padding(
    padding: const EdgeInsets.all(16),
    child: Text('Details for row $index'),
  ),
  columns: [ /* ... */ ],
  rows: _rows,
)
```

### Collapsible groups

```dart
FlexTable(
  collapsedGroups: _collapsed,
  onGroupToggled: (index) => setState(() {
    _collapsed.contains(index)
        ? _collapsed.remove(index)
        : _collapsed.add(index);
  }),
  groups: [
    FlexTableGroup(
      header: Text('Fruits'),
      startIndex: 0,
      endIndex: 2,
      collapsible: true,
    ),
    FlexTableGroup(
      header: Text('Vegetables'),
      startIndex: 3,
      endIndex: 5,
      collapsible: true,
    ),
  ],
  columns: [ /* ... */ ],
  rows: _rows,
)
```

### Striped theme

```dart
FlexTable(
  theme: FlexTableTheme.striped(context),
  columns: [ /* ... */ ],
  rows: _rows,
)
```

### Hide a column at runtime

```dart
FlexTableColumn(
  header: Text('Internal ID'),
  visible: _showId,   // toggle this to show/hide the column
)
```

### Footer row

```dart
FlexTable(
  footerRows: [
    FlexTableRow(cells: [Text('Total'), Text('\$99.00')]),
  ],
  columns: [ /* ... */ ],
  rows: _rows,
)
```

### Custom theme

```dart
FlexTable(
  theme: FlexTableTheme.defaultTheme(context).copyWith(
    cellPadding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
    headerTextStyle: TextStyle(fontWeight: FontWeight.w900),
    rowDivider: BorderSide(color: Colors.grey.shade200),
  ),
  columns: [ /* ... */ ],
  rows: _rows,
)
```

## Additional information

- The table has **no built-in scrolling**. Wrap it in a `SingleChildScrollView`
  (horizontal and/or vertical) when content may overflow.
- File issues and feature requests on
  [GitHub](https://github.com/Miso-0/flex_table/issues).
- Contributions are welcome — please open a PR with tests for any new behaviour.
