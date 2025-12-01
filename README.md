# OpenCart Product Tag Filter

OCMOD extension that adds tag filtering to the admin product list page for OpenCart 3.x.

**GitHub**: https://github.com/ozhound/opencart-product-tag-filter

## Installation

1. Upload `upload/system/product_tag_filter.ocmod.xml` via Extensions → Installer
2. Go to Extensions → Modifications and click Refresh
3. Clear cache (Dashboard → Gear Icon → Refresh both)

## Usage

Navigate to Catalog → Products and use the new "Tag" filter field.

## Compatibility

- OpenCart 3.0.x
- Tested on 3.0.4.1

## What it does

Adds a tag filter field to the admin product list that:
- Searches product tags
- Supports partial matching
- Maintains filter state across pagination
- Uses OCMOD (no core file modifications)
