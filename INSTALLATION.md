# Installation Guide

Complete step-by-step installation guide for the OpenCart Product Tag Filter extension.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Pre-Installation Steps](#pre-installation-steps)
3. [Installation Methods](#installation-methods)
4. [Post-Installation](#post-installation)
5. [Verification](#verification)
6. [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before installing this extension, ensure you have:

- ✅ OpenCart version 3.0.x installed
- ✅ Admin panel access
- ✅ FTP/File Manager access (for manual installation)
- ✅ Backup of your site (recommended)

**Check your OpenCart version:**
1. Login to Admin Panel
2. Look at bottom-left footer - should show "OpenCart 3.0.x.x"

---

## Pre-Installation Steps

### 1. Backup Your Store

**Database Backup:**
```bash
# Via phpMyAdmin: Export → Quick → Go
# Via command line:
mysqldump -u username -p database_name > backup_$(date +%Y%m%d).sql
```

**File Backup (Optional):**
Backup these files as a precaution:
- `admin/model/catalog/product.php`
- `admin/controller/catalog/product.php`
- `admin/view/template/catalog/product_list.twig`

### 2. Verify File Permissions

Ensure the `system/` directory is writable:

**Via FTP:**
- Right-click `system/` folder → File Permissions → Set to `755` or `775`

**Via SSH:**
```bash
chmod 755 system/
```

---

## Installation Methods

### Method A: Extension Installer (Recommended)

#### Step 1: Download the Extension

Download `product_tag_filter.ocmod.xml` from:
- [Latest Release](../../releases/latest)
- Or directly from `/upload/system/product_tag_filter.ocmod.xml`

#### Step 2: Upload via Admin Panel

1. **Login** to OpenCart Admin Panel

2. **Navigate** to Extensions:
   ```
   Extensions → Installer
   ```

3. **Upload File**:
   - Click the blue "Upload" button
   - Select `product_tag_filter.ocmod.xml`
   - Click "Continue"
   - Wait for "Success" message

   ![Upload Success](https://via.placeholder.com/600x100?text=Success+Message)

#### Step 3: Enable the Modification

1. **Navigate** to Modifications:
   ```
   Extensions → Modifications
   ```

2. **Refresh** Modifications:
   - Click the blue 🔄 "Refresh" button (top-right corner)
   - This rebuilds the modification cache
   - Wait for the page to reload

3. **Verify** Installation:
   - Look for "Admin Product Tag Filter" in the modification list
   - Status should show as enabled (green checkmark)

   | Name | Author | Version | Date Added | Action |
   |------|--------|---------|------------|--------|
   | Admin Product Tag Filter | OpenCart Community | 1.0.0 | [Today's Date] | 🗑️ |

#### Step 4: Clear All Caches

1. **Navigate** to Dashboard:
   ```
   Dashboard (click the home icon)
   ```

2. **Click** the blue gear/cog icon (⚙️) in top-right corner

3. **Clear Caches**:
   - Click "Refresh" next to the Orange gear (Theme Cache)
   - Click "Refresh" next to the Blue gear (Modification Cache)
   - Both should show success messages

---

### Method B: Manual FTP Installation

#### Step 1: Download the Extension

Download `product_tag_filter.ocmod.xml` from the repository

#### Step 2: Upload via FTP

1. **Connect** to your server via FTP (using FileZilla, WinSCP, etc.)

2. **Navigate** to your OpenCart root directory

3. **Upload** the file:
   ```
   Upload: product_tag_filter.ocmod.xml
   To: /system/product_tag_filter.ocmod.xml
   ```

4. **Verify** upload:
   - File should appear in `system/` directory
   - File size should be ~5-6 KB

#### Step 3: Enable via Admin Panel

1. **Login** to Admin Panel

2. **Navigate** to:
   ```
   Extensions → Modifications
   ```

3. **Refresh** Modifications:
   - Click the blue 🔄 "Refresh" button
   - The system will detect the new OCMOD file automatically

4. **Verify** "Admin Product Tag Filter" appears in the list

#### Step 4: Clear Caches

Same as Method A, Step 4

---

### Method C: SSH/Command Line Installation

```bash
# Navigate to OpenCart root
cd /path/to/opencart

# Download the file
wget https://github.com/yourusername/opencart-product-tag-filter/raw/main/upload/system/product_tag_filter.ocmod.xml -O system/product_tag_filter.ocmod.xml

# Set permissions
chmod 644 system/product_tag_filter.ocmod.xml

# Verify
ls -la system/product_tag_filter.ocmod.xml
```

Then follow Method B, Steps 3-4

---

## Post-Installation

### Verify Extension is Active

1. **Check Modifications List**:
   ```
   Extensions → Modifications
   ```
   - "Admin Product Tag Filter" should be listed
   - No error icons should appear

2. **Check Modification Log** (if available):
   ```
   Extensions → Modifications → View Log
   ```
   - Should show no errors
   - Should show successful file modifications

---

## Verification

### Test the Filter

1. **Navigate** to Product List:
   ```
   Catalog → Products
   ```

2. **Locate the Filter Section**:
   - Look for the filter panel at the top
   - You should see filter fields: Name, Model, **Tag**, Price, Quantity, Status

3. **Test Filtering**:

   **Step 1:** Find a product with tags
   - Click "Edit" on any product
   - Go to "Data" tab
   - Note the tags (e.g., "summer, beach, vacation")
   - Click "Cancel" to return

   **Step 2:** Use the filter
   - In the "Tag" field, enter one of the tags (e.g., "beach")
   - Click the blue "Filter" button
   - Products with matching tags should appear

4. **Test Partial Matching**:
   - Enter partial tag (e.g., "bea" for "beach")
   - Click "Filter"
   - Should still return matching products

5. **Test Pagination**:
   - Apply a tag filter that returns multiple pages
   - Navigate to page 2
   - Filter should remain active

---

## Troubleshooting

### Filter Field Not Showing

**Problem**: Tag filter field doesn't appear after installation

**Solutions**:

1. **Clear Browser Cache**:
   ```
   Ctrl + Shift + Delete (Chrome/Firefox)
   Cmd + Shift + Delete (Safari)
   ```

2. **Clear Server Cache**:
   ```
   Dashboard → Gear Icon → Refresh (both buttons)
   ```

3. **Verify Modification is Enabled**:
   ```
   Extensions → Modifications → Look for green checkmark
   ```

4. **Check for Errors**:
   ```
   Extensions → Modifications → Check for red error icons
   ```

5. **Re-apply Modification**:
   ```
   Extensions → Modifications → Refresh
   ```

---

### Upload Failed Error

**Problem**: "Upload failed" or "Invalid file" error

**Solutions**:

1. **Check File Format**:
   - File must be `.ocmod.xml`
   - File must be valid XML (not corrupted)

2. **Check File Size**:
   - File should be 5-6 KB
   - If 0 KB, re-download

3. **Check Server Upload Limits**:
   ```php
   // Check php.ini
   upload_max_filesize = 2M
   post_max_size = 8M
   ```

4. **Try Manual Installation** (Method B)

---

### Modification Not Listed

**Problem**: Extension doesn't appear in Modifications list

**Solutions**:

1. **Verify File Location**:
   ```
   File should be in: system/product_tag_filter.ocmod.xml
   Not in: system/storage/ or other subdirectories
   ```

2. **Check XML Validity**:
   - Open file in text editor
   - Ensure XML structure is intact
   - Look for `<modification>` opening and closing tags

3. **Check File Permissions**:
   ```bash
   chmod 644 system/product_tag_filter.ocmod.xml
   ```

4. **Force Refresh**:
   - Go to Extensions → Modifications
   - Click Refresh multiple times
   - Check if it appears

---

### Search Returns No Results

**Problem**: Filter doesn't return any products with tags

**Solutions**:

1. **Verify Products Have Tags**:
   - Edit a product
   - Go to "Data" tab
   - Check if "Meta Tag Keywords" or "Tags" field has values
   - Tags should be comma-separated

2. **Check Tag Format**:
   ```
   Correct: summer, beach, vacation
   Incorrect: #summer #beach (hashtags not needed)
   ```

3. **Test with Known Tag**:
   - Find a product you know has tags
   - Copy exact tag text
   - Paste into filter
   - Click Filter

4. **Check Database**:
   ```sql
   SELECT product_id, tag 
   FROM oc_product_description 
   WHERE tag IS NOT NULL AND tag != '';
   ```

---

### Conflicts with Other Extensions

**Problem**: Other extensions stop working after installation

**Solutions**:

1. **Check Modification Priority**:
   ```
   Extensions → Modifications
   Check order - last installed = highest priority
   ```

2. **Identify Conflicting Extension**:
   - Disable this extension
   - Test other extensions
   - Re-enable this extension
   - Check modification log for conflicts

3. **Contact Support**:
   - Report issue on GitHub
   - Provide list of installed extensions
   - Include modification log

---

## Rollback/Uninstallation

If you need to remove the extension:

### Quick Uninstall

1. **Navigate** to:
   ```
   Extensions → Modifications
   ```

2. **Delete Modification**:
   - Find "Admin Product Tag Filter"
   - Click red 🗑️ "Delete" button
   - Confirm deletion

3. **Refresh**:
   - Click blue 🔄 "Refresh" button
   - Clear cache (Dashboard → Gear Icon → Refresh)

### Complete Removal

1. **Delete OCMOD file via FTP**:
   ```
   Delete: system/product_tag_filter.ocmod.xml
   ```

2. **Clear modifications**:
   ```
   Extensions → Modifications → Refresh
   ```

3. **Restore backup** (if needed)

---

## Support

If you encounter issues not covered here:

1. **Check GitHub Issues**: [Report Issue](../../issues)
2. **OpenCart Forum**: [Community Support](https://forum.opencart.com/)
3. **Review Documentation**: [README](README.md)

---

**Installation Date**: _______________  
**Installed By**: _______________  
**OpenCart Version**: _______________  
**Extension Version**: 1.0.0
