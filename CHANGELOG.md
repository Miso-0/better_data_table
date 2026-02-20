## 0.1.0

Initial public release.

**New features:**
- `FlexTableColumn.visible` — hide/show individual columns at runtime
- `FlexTableColumn.tooltip` — tooltip on column header
- `FlexTableColumn.minWidth` / `maxWidth` — now actually enforced via
  `MaxColumnWidth` / `MinColumnWidth` wrappers
- `FlexTableColumn.copyWith()`
- `FlexTableRow.tooltip` — tooltip on hover over entire row
- `FlexTableRow.copyWith()`
- `FlexTableGroup.collapsible` — users can collapse/expand groups;
  controlled via `FlexTable.collapsedGroups` + `onGroupToggled`
- `FlexTableGroup.copyWith()`
- `FlexTable.onRowSecondaryTap` — right-click / secondary tap callback
- `FlexTable.rowDivider` (`BorderSide?`) — full-width row divider drawn as
  a bottom border on each data row (replaces the broken single-cell `divider`)
- `FlexTable.collapsedGroups` + `FlexTable.onGroupToggled`

**Fixed:**
- `FlexTableTheme.striped` now actually applies alternating row colors
- `alternateRowDecoration` is now used for odd-indexed rows
- `cellTextStyle` is now applied to every data cell via `DefaultTextStyle.merge`
- `minWidth` / `maxWidth` on columns were defined but had no effect — fixed
- Expand toggle now has a circular `InkWell` splash for better touch feedback

**Structural:**
- Split into `lib/src/` modules (`flex_table_column.dart`,
  `flex_table_row.dart`, `flex_table_group.dart`, `flex_table_theme.dart`,
  `flex_table_widget.dart`) with a clean barrel export in `lib/flex_table.dart`
- 46 widget and unit tests added
