# Base Table Component

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This component manages the base table structure, providing a flexible and customizable table component for various use cases.</p>
  <img src="basetable.png" alt="Flowchart of Base Table Component"/>
</tldr>

<procedure title="To manage the base table component:" id="procedure-id-base-table">
   <step>Initialize the table state and configuration.</step>
   <step>Render the table with headers, rows, and cells based on the provided data and columns.</step>
   <step>Handle user interactions such as sorting, filtering, and pagination.</step>
   <step>Update the table state and re-render the table as needed.</step>
   <p>Congratulations! You have successfully managed the base table component.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a> !</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the table state and configuration are correctly initialized and managed.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the component.

## Sequence and Flow

1. **Import Dependencies**:
- The necessary modules and utilities are imported, including `Pagination`, `useReactTable`, `toCSV`, `toJSON`, and various UI components.

2. **Initialize Table State**:
- The table state and configuration are initialized, including column visibility and pagination settings.

3. **Render Table**:
- The table is rendered with headers, rows, and cells based on the provided data and columns.

4. **Handle User Interactions**:
- User interactions such as sorting, filtering, and pagination are handled, updating the table state accordingly.

5. **Update and Re-render Table**:
- The table state is updated and the table is re-rendered as needed.

<img src="sequence.png" alt="Sequence Diagram of Base Table Component"/>

## Example Code

```typescript
import Pagination from './pagination';
import {
  ColumnDef,
  flexRender,
  VisibilityState,
  getCoreRowModel,
  useReactTable
} from '@tanstack/react-table';
import { useState } from 'react';
import { toCSV, toJSON } from '@/lib/export';
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow
} from '@/components/ui/table';
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectSeparator,
  SelectTrigger,
  SelectValue
} from '@/components/ui/select';
import {
  DropdownMenu,
  DropdownMenuCheckboxItem,
  DropdownMenuContent,
  DropdownMenuTrigger
} from '@/components/ui/dropdown-menu';
import { Input } from '@/components/ui/input';
import { Button } from '@/components/ui/button';

import type { TableLimit } from '@/lib/hooks';

interface DataTableProps<TData, TValue> {
  title?: string;
  states: {
    query: string;
    limit: TableLimit;
    page: number;
  };
  setStates: {
    setQuery: React.Dispatch<React.SetStateAction<string>>;
    setLimit: React.Dispatch<React.SetStateAction<TableLimit>>;
    setPage: React.Dispatch<React.SetStateAction<number>>;
  };
  columns: ColumnDef<TData, TValue>[];
  resp?: {
    total: number;
    data: TData[];
  };
}

export function DataTable<TData, TValue>({
  title,
  states,
  setStates,
  columns,
  resp
}: DataTableProps<TData, TValue>) {
  const [columnVisibility, setColumnVisibility] = useState<VisibilityState>({});

  const table = useReactTable({
    data: resp?.data || [],
    columns,
    getCoreRowModel: getCoreRowModel(),
    onColumnVisibilityChange: setColumnVisibility,
    state: {
      columnVisibility
    }
  });

  const pageCount = Math.ceil((resp?.total ?? 0) / Number(states.limit));
  const tableData = table.getRowModel().rows.map((row) => row.original);

  const handleValueChange = (val: TableLimit) => {
    setStates.setLimit(val);
    const newPageCount = Math.ceil((resp?.total ?? 0) / Number(val));
    if (states.page > newPageCount) setStates.setPage(newPageCount);
  };

  return (
    <div className="flex flex-col gap-1.5">
      <div className="flex items-center justify-between">
        <div className="flex items-center gap-6">
          {title && <h1 className="text-2xl font-semibold">{title}</h1>}

          <Input
            placeholder="Search..."
            className="w-64"
            onChange={(e) => setStates.setQuery(e.target.value)}
          />
        </div>
        <div className="flex items-center gap-2">
          <Button variant="outline" onClick={() => toCSV(tableData)}>
            Export to CSV
          </Button>
          <Button variant="outline" onClick={() => toJSON(tableData)}>
            Export to JSON
          </Button>

          <Select value={states.limit} onValueChange={handleValueChange}>
            <SelectTrigger>
              <SelectValue placeholder="Max Rows" />
            </SelectTrigger>
            <SelectContent>
              <SelectGroup>
                <SelectLabel>Max Rows</SelectLabel>
                <SelectSeparator />
                {(['10', '15', '20', '50', '100'] as TableLimit[]).map(
                  (limit) => (
                    <SelectItem key={limit} value={limit}>
                      {limit}
                    </SelectItem>
                  )
                )}
              </SelectGroup>
            </SelectContent>
          </Select>

          <DropdownMenu>
            <DropdownMenuTrigger asChild>
              <Button variant="outline" className="ml-auto">
                Columns
              </Button>
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end">
              {table
                .getAllColumns()
                .filter((column) => column.getCanHide())
                .map((column) => {
                  return (
                    <DropdownMenuCheckboxItem
                      key={column.id}
                      className="capitalize"
                      checked={column.getIsVisible()}
                      onCheckedChange={(value) =>
                        column.toggleVisibility(!!value)
                      }
                      onSelect={(e) => e.preventDefault()}
                    >
                      {column.id}
                    </DropdownMenuCheckboxItem>
                  );
                })}
            </DropdownMenuContent>
          </DropdownMenu>
        </div>
      </div>
      <div className="rounded-md border">
        <Table>
          <TableHeader>
            {table.getHeaderGroups().map((headerGroup) => (
              <TableRow key={headerGroup.id}>
                {headerGroup.headers.map((header) => {
                  return (
                    <TableHead key={header.id}>
                      {header.isPlaceholder
                        ? null
                        : flexRender(
                            header.column.columnDef.header,
                            header.getContext()
                          )}
                    </TableHead>
                  );
                })}
              </TableRow>
            ))}
          </TableHeader>
          <TableBody>
            {table.getRowModel().rows?.length ? (
              table.getRowModel().rows.map((row) => (
                <TableRow
                  key={row.id}
                  data-state={row.getIsSelected() && 'selected'}
                >
                  {row.getVisibleCells().map((cell) => (
                    <TableCell key={cell.id}>
                      {flexRender(
                        cell.column.columnDef.cell,
                        cell.getContext()
                      )}
                    </TableCell>
                  ))}
                </TableRow>
              ))
            ) : (
              <TableRow>
                <TableCell
                  colSpan={columns.length}
                  className="h-24 text-center"
                >
                  No results.
                </TableCell>
              </TableRow>
            )}
          </TableBody>
        </Table>
      </div>

      <Pagination
        page={states.page}
        setPage={setStates.setPage}
        pageCount={pageCount}
      />
    </div>
  );
}