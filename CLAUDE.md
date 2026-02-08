# CLAUDE.md

## Project Overview

This repository contains reference materials and documentation for a **1C:Enterprise** (1С:Предприятие) development project. The project focuses on building a data processing tool ("обработка") for **loading nomenclature items and creating initial balance documents** (ВводНачальныхОстатков — VNO) in a 1C:Enterprise system.

This is **not a software source code repository** — it stores specifications, queries, and visual references used during 1C development.

## Repository Contents

| File | Description |
|------|-------------|
| `запрос.xls` | Excel spreadsheet containing a query/request definition, likely a data query template for the 1C processing |
| `изображение.png` | Screenshot of the 1C data processing form "ЗагрузкаНоменклатурыИСоздатьДокументВНО" — shows form layout, requisites (attributes), and their types |
| `параметры реквизита партия.jpg` | Screenshot showing configuration of the "Партия" (Batch/Lot) attribute — type `ДокументСсылка.ПервичныйДокумент`, with selection filters for document types |

## 1C Processing Details

The main data processing object documented here is **"ЗагрузкаНоменклатурыИСоздатьДокументВНО"** (Load Nomenclature and Create Initial Balance Document). Key elements:

### Form Structure
- **КоманднаяПанель** — Command panel
- **ГруппаЗагрузитьНоменклатуруИСоздатьДокументВНО** — Main group with fields:
  - `Склад` (Warehouse) — `СправочникСсылка.Склады`
  - `Организация` (Organization) — `СправочникСсылка.Организации`
  - `СоздатьВВодНачальныхОстатков` — Button/command to create initial balances
- **ГруппаЗагрузкаКартинок** — Image upload group
- **КомандаЗагрузитьИзCSV** — CSV import command
- **ТабличныйДокумент** — Spreadsheet/table section with search and browse controls

### Object Requisites (Attributes)
- `ИмяФайлаДляЗагрузки` — File name for import (String)
- `Организация` — Organization (String)
- `ПерваяСтрокаДанныхТабличногоДокумента` — First data row number (Number)
- `ВидЦеныНовогоДокумента` — Price type for new document (String)
- `НеСоздаватьНоменклатуру` — Do not create nomenclature (Boolean)
- `ДобавитьШК` — Add barcode (Boolean)
- `НеОбновлятьДопРеквНоменклатуры` — Do not update additional nomenclature attributes (Boolean)
- `ПутьКПапкеИзображений` — Path to images folder (String)

### Tabular Document Columns
- `НомерСтроки` — Row number (Number)
- `Артикул` — Article/SKU (String)
- `ШтрихКод` — Barcode (String)
- `Наименование` — Name (`СправочникСсылка.Номенклатура`)
- `Характеристика` — Characteristic (String)
- `ВидНоменклатуры` — Nomenclature type (String)
- `ЦенаЗакупочная` — Purchase price (String)
- `Кол_во` — Quantity (String)
- `GUIDBБазеИсточнике` — GUID in source database (String)
- `GuidНоменклатурыВБазеИсточнике` — Nomenclature GUID in source database (String)
- `КоличествоСтрок` — Row count (Number, aggregate)

### "Партия" (Batch) Attribute Configuration
- **Type**: `ДокументСсылка.ПервичныйДокумент` (DocumentRef.PrimaryDocument)
- **Selection parameter links**: `Отбор.Организация(Организация)`
- **Selection parameters**: Filters by `ТипПервичногоДокумента` — `ПриобретениеУПоставщика`, `ВнутренняяНакладная`, `ПриемНаХранение`
- **Tooltip**: "Партия товаров" (Goods batch)
- **Full-text search**: Enabled
- **Data history**: Enabled

## Conventions

- **File names** are in Russian (Cyrillic) — this is standard for 1C:Enterprise projects
- **Binary files only** — the repository stores Excel and image files, not 1C source code (`.bsl`, `.xml`)
- **Commit messages** should describe what reference material was added or updated

## Development Workflow

1. Capture screenshots and export queries from the 1C:Enterprise Configurator
2. Add reference files to this repository
3. Use these specifications when implementing the data processing in 1C:Enterprise

## Tools & Environment

- **Platform**: 1C:Enterprise 8.x
- **File formats**: XLS (Excel 97-2003), PNG, JPEG
- **Language**: Russian (all identifiers and documentation are in Russian)
