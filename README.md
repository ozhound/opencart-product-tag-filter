# OpenCart Product Tag Filter Extension

[![OpenCart Version](https://img.shields.io/badge/OpenCart-3.0.x-blue.svg)](https://www.opencart.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![OCMOD](https://img.shields.io/badge/Type-OCMOD-orange.svg)](https://docs.opencart.com/en-gb/extension/modifications/)

Add tag filtering capability to the OpenCart 3.x admin product list page. This extension allows administrators to quickly filter products by tags without modifying core files.

## Features

✅ **Non-invasive**: Uses OpenCart's OCMOD system - no core file modifications  
✅ **Easy Installation**: Install via Extension Installer  
✅ **Update Safe**: Survives OpenCart updates  
✅ **Partial Matching**: Searches for partial tag matches  
✅ **Admin Only**: Adds filter to admin panel product list  
✅ **Lightweight**: Single OCMOD XML file  

## Screenshots

*Filter field appears in the admin product list alongside existing filters (Name, Model, Price, etc.)*

## Requirements

- **OpenCart Version**: 3.0.x (Tested on 3.0.4.1)
- **PHP Version**: 5.4+ (as per OpenCart 3.0.x requirements)
- **Admin Access**: Required for installation

## Installation

### Method 1: Via Extension Installer (Recommended)

1. **Download** the `product_tag_filter.ocmod.xml` file from the [Releases](../../releases) page or from `upload/system/`

2. **Login** to your OpenCart Admin Panel

3. **Navigate** to `Extensions` → `Installer`

4. **Upload** the XML file:
   - Click the "Upload" button
   - Select `product_tag_filter.ocmod.xml`
   - Click "Continue"

5. **Apply** the modification:
   - Go to `Extensions` → `Modifications`
   - Click the blue "Refresh" button (🔄 icon in top-right corner)
   - Verify "Admin Product Tag Filter" appears in the modification list

6. **Clear Cache**:
   - Go to `Dashboard`
   - Click the blue gear/cog icon (top-right)
   - Click both "Refresh" buttons to clear cache

### Method 2: Manual Installation (FTP)

1. **Download** the repository or just the OCMOD XML file

2. **Upload** via FTP:
   - Upload `product_tag_filter.ocmod.xml` to your server's `system/` directory

3. **Apply** the modification:
   - Login to Admin Panel
   - Go to `Extensions` → `Modifications`
   - Click the "Refresh" button
   - Verify the modification appears in the list

4. **Clear Cache** (same as Method 1, step 6)

## Usage

1. Navigate to `Catalog` → `Products` in your admin panel

2. Look for the new **"Tag"** filter field in the filter section (appears after the Model filter)

3. Enter a tag (or partial tag) you want to search for

4. Click the **"Filter"** button

5. Products matching the tag will be displayed

### Example

If you have products tagged with:
- "summer, beach, vacation"
- "winter, snow, cold"
- "summer, pool"

Searching for **"summer"** will return products 1 and 3.

## How It Works

According to [OpenCart's OCMOD documentation](https://docs.opencart.com/en-gb/extension/modifications/), this extension uses XML modifications to:

1. **Model Layer** (`admin/model/catalog/product.php`):
   - Adds `filter_tag` parameter to the SQL WHERE clause
   - Uses `LIKE '%tag%'` for partial matching
   - Implements `$this->db->escape()` for SQL injection prevention

2. **Controller Layer** (`admin/controller/catalog/product.php`):
   - Captures `filter_tag` from GET request
   - Passes it to the model's `getProducts()` method
   - Maintains filter state across pagination

3. **View Layer** (`admin/view/template/catalog/product_list.twig`):
   - Adds new input field for tag filtering
   - Matches existing filter field styling
   - Preserves tag value after filtering

## Troubleshooting

### Modification doesn't appear after installation

**Solution**:
1. Check file permissions - ensure `system/` directory is writable
2. Clear your browser cache
3. Check `Extensions` → `Modifications` for any error logs

### Filter field not showing

**Solution**:
1. Ensure you clicked "Refresh" in `Extensions` → `Modifications`
2. Clear modification cache: `Dashboard` → Gear Icon → Refresh
3. Clear theme cache: `Dashboard` → Gear Icon → Refresh
4. Check that the modification is enabled in the modification list

### Search not working

**Solution**:
1. Verify your products have tags assigned (edit a product and check the "Data" tab)
2. Tags are case-insensitive - try different variations
3. Check modification log for SQL errors

### Conflicts with other extensions

**Solution**:
1. Check `Extensions` → `Modifications` for error messages
2. This extension modifies standard filter areas - conflicts are rare
3. If conflicts occur, check modification priority order

## Uninstallation

1. Go to `Extensions` → `Modifications`
2. Find "Admin Product Tag Filter" in the list
3. Click the red "Delete" button (🗑️ icon)
4. Click "Refresh" to rebuild modifications
5. Clear cache

## Compatibility

| OpenCart Version | Status |
|-----------------|--------|
| 3.0.4.1 | ✅ Tested |
| 3.0.3.x | ✅ Compatible |
| 3.0.2.x | ✅ Compatible |
| 3.0.1.x | ✅ Compatible |
| 3.0.0.x | ✅ Compatible |
| 2.3.x | ❌ Not Compatible |
| 4.x | ❌ Not Compatible (different structure) |

## Technical Details

### Database Schema

Tags are stored in the `product_description` table:
```sql
SELECT * FROM oc_product_description WHERE tag LIKE '%yourtag%';
```

### Security

- Uses OpenCart's built-in `$this->db->escape()` for SQL injection prevention
- Implements `html_entity_decode()` for XSS protection on URL parameters
- No direct database queries - uses OpenCart's database abstraction layer

### Performance

- Minimal performance impact
- Uses existing database indexes
- No additional database tables required

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Test thoroughly on OpenCart 3.0.x
4. Commit your changes (`git commit -am 'Add new feature'`)
5. Push to the branch (`git push origin feature/improvement`)
6. Create a Pull Request

## Support

- **Issues**: [GitHub Issues](../../issues)
- **OpenCart Forum**: [OpenCart Community](https://forum.opencart.com/)
- **Documentation**: [OpenCart Official Docs](https://docs.opencart.com/)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

## Credits

- Developed following [OpenCart OCMOD Best Practices](https://docs.opencart.com/en-gb/extension/modifications/)
- Based on OpenCart's extension development guidelines
- Community feedback and testing

## Disclaimer

This extension modifies admin functionality only. Always test on a development/staging environment before deploying to production.

---

**Found this useful? ⭐ Star this repo!**
