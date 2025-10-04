Here's the updated README.md file with all the new changes:

```markdown
# HotBird – Menu Management Guide

This guide explains how to manage the menu items for the **HotBird website** by editing the associated JSON files.

---

## 1. Menu Data Structure

The menu items are organized into several JSON files, each representing a category. These files are loaded dynamically by the website to display the menu.

**List of JSON Files:**

* `hotbirds.json`
* `hotbuckets.json`
* `wings.json`
* `drinks.json`
* `sauces.json`
* `hot-tenders.json` ⭐ **NEW**
* `hot-deals.json` ⭐ **NEW**

⚠️ **Important:** All JSON files must be located in the same directory as `index.html`.
Images for menu items are stored in the `images/` folder, so the `image` field should point to `images/YourImageName.jpg`.

---

## 2. Understanding a Menu Item JSON Object

### Standard Item Example:
```json
{
  "name": "Chicken Tenders or Wings",
  "description": "Chicken wings or tenders with any 1 sauce",
  "image": "images/Wings.png",
  "tags": ["wings", "chicken"],
  "mealPriceModifier": 2.50,
  "options": [
    { "name": "5 piece", "price": 5.00 },
    { "name": "10 piece", "price": 9.00 },
    { "name": "15 piece", "price": 14.00 },
    { "name": "20 piece", "price": 18.00 }
  ],
  "showSlider": false,
  "sauces": true,
  "vegetables": false
}
```

### Combo Deal Example (NEW):
```json
{
  "name": "Bird's Feast Combo",
  "description": "Perfect for sharing - includes tenders, wings, fries, and drinks",
  "image": "images/Birds Feast Combo.jpg",
  "price": 18.50,
  "tags": ["hotdeals", "combo"],
  "mealPriceModifier": 0.00,
  "showSlider": false,
  "sauces": false,
  "vegetables": false,
  "comboItems": [
    {
      "name": "Classic Hot Tenders",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Chicken Tenders or Wings",
      "option": "10 piece",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Fries",
      "quantity": 2,
      "includedInCombo": true
    },
    {
      "name": "Pepsi",
      "quantity": 2,
      "includedInCombo": true
    }
  ]
}
```

### Field Explanations

* **name**: Name of the menu item. *(string)*
* **description**: Short description displayed under the name. *(string)*
* **image**: Filename of the image (must exist in the `images/` folder). *(string)*
  e.g. `"images/Chocolate Milkshake.jpg"`
* **tags**:
  * Used for categorization and filtering.
  * First tag = badge on menu card.
  * Special tags:
    * `"D"` → Drinks (centered images, scaled properly for cans).
    * `"M"` → Milkshakes (image scaled fully outward to show full picture on all screen sizes).
    * `"combo"` → Combo deals (shows included items in modal).
* **mealPriceModifier**: Extra cost when upgrading to a meal. *(decimal)*
* **options** *(optional)*: Variations of the item.
  * **Special behavior:**
    * If *all options* have prices → price shows on the **button**.
    * If *not all options* have prices → price shows in the **dropdown**.
* **showSlider**: Always set to `false` (legacy field).
* **sauces**: `true`/`false` – whether customer can choose sauces.
* **vegetables**: `true`/`false` – whether customer can choose vegetables.
* **comboItems** ⭐ **NEW**: Array of items included in a combo deal. Only for `hotdeals` category.
  * **name**: Name of included item (must match existing menu item names)
  * **quantity**: How many of this item are included
  * **option** *(optional)*: Specific option/variant if applicable
  * **includedInCombo**: Always `true`

---

## 3. Image Rules

* **Size**: All images must be **1200 × 1200 px**.
* **Format**: `.jpg` or `.png`.
* **Location**: All images go inside the `images/` folder.
* **Naming**: Must match exactly the `image` field in JSON (case-sensitive), including the `images/` prefix.

**Special Cases:**

* **Drinks** (`"D"` tag): Canned drinks centered properly.
* **Milkshakes** (`"M"` tag): Full image always shown, scaled outward.
* **Combo Deals** (`"combo"` tag): Show included items list when clicked.
* **All Other Items**: Positioned according to Website Manager's preferences.

---

## 4. Editing Workflow

1. Identify which JSON file contains the category.
2. Copy an existing item as a template.
3. Edit `name`, `description`, `image`, `tags`, `price/options`.
4. **For combo deals**: Add `comboItems` array with included items.
5. Save the JSON file.
6. Add the image file (1200×1200 px) to the `images/` folder.
7. **Use the JSON Converter Tool** (see below) to validate and format your JSON.
8. Refresh the website to see changes.

---

## 5. JSON Converter Tool

For easy JSON creation and validation, use our online JSON Converter:

🔗 **HotBird JSON Converter:** [https://json-convertor-hot-bird.vercel.app](https://json-convertor-hot-bird.vercel.app)

This tool provides:
- **GUI-based JSON editing** - No manual coding required
- **Real-time validation** - Catch errors before saving
- **Template generation** - Start with pre-built item templates
- **Formatting assistance** - Ensure proper JSON structure
- **Copy-paste functionality** - Easy transfer to your files
- **Combo item support** ⭐ **NEW** - Add included items to combo deals

**Recommended workflow:** Use the converter to create/validate items, then copy the output into your JSON files.

---

## 6. Examples

### Drink Example (Pepsi)
```json
{
  "name": "Pepsi",
  "description": "Refreshing cold Pepsi drink",
  "image": "images/Pepsi.jpg",
  "price": 1.50,
  "tags": ["drinks", "D"],
  "mealPriceModifier": 0.00,
  "showSlider": false,
  "sauces": false,
  "vegetables": false
}
```

### Milkshake Example
```json
{
  "name": "Chocolate Milkshake",
  "description": "Rich and creamy chocolate milkshake",
  "image": "images/Chocolate Milkshake.jpg",
  "price": 3.50,
  "tags": ["drinks", "dessert", "M"],
  "mealPriceModifier": 0.00,
  "showSlider": false,
  "sauces": false,
  "vegetables": false
}
```

### Burger with Options Example
```json
{
  "name": "Double Smash Beef Burger",
  "description": "Double smashed beef patties with cheese and special sauce",
  "image": "images/Double Smash Beef Burger.jpg",
  "price": 9.00,
  "tags": ["hotbuckets", "burger", "beef"],
  "mealPriceModifier": 2.50,
  "showSlider": false,
  "sauces": true,
  "vegetables": false
}
```

### Hot Tenders Example ⭐ **NEW**
```json
{
  "name": "Classic Hot Tenders",
  "description": "Crispy, juicy chicken tenders with your choice of dip",
  "image": "images/Classic Hot Tenders.jpg",
  "price": 6.50,
  "tags": ["hottenders", "chicken"],
  "mealPriceModifier": 2.50,
  "showSlider": false,
  "sauces": true,
  "vegetables": false
}
```

### Combo Deal Example ⭐ **NEW**
```json
{
  "name": "Family Feast Deal",
  "description": "Everything for the whole family - burgers, tenders, wings, and more",
  "image": "images/Family Feast Deal.jpg",
  "price": 32.00,
  "tags": ["hotdeals", "combo"],
  "mealPriceModifier": 0.00,
  "showSlider": false,
  "sauces": false,
  "vegetables": false,
  "comboItems": [
    {
      "name": "Double Smash Beef Burger",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Nash Crunch Burger",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Hot Tenders Platter",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Chicken Tenders or Wings",
      "option": "15 piece",
      "quantity": 1,
      "includedInCombo": true
    },
    {
      "name": "Fries",
      "quantity": 3,
      "includedInCombo": true
    },
    {
      "name": "Assorted Drinks",
      "quantity": 4,
      "includedInCombo": true
    }
  ]
}
```

---

## 7. Order Payload Examples for Backend

#### 1. Single Smash Beef Burger (no meal):
```json
{
  "deliveryType": "collection",
  "customer": {
    "fullName": "Jane Smith",
    "phone": "555-1234",
    "email": "jane@example.com",
    "specialInstructions": "No onions please"
  },
  "items": [
    {
      "name": "Single Smash Beef Burger with Burger Blast",
      "price": 7.00,
      "quantity": 1,
      "selectedSauce": "Burger Blast"
    }
  ],
  "total": "7.00"
}
```

#### 2. Chicken Tenders with Chips & Drink (Sprite):
```json
{
  "deliveryType": "collection",
  "customer": {
    "fullName": "John Doe",
    "phone": "123-456-7890",
    "email": "john@example.com"
  },
  "items": [
    {
      "name": "Chicken Tenders or Wings (10 piece) with Buffalo Kick",
      "price": 9.00,
      "quantity": 1,
      "selectedOption": "10 piece",
      "selectedSauce": "Buffalo Kick"
    },
    {
      "name": "Chips & Drink (Sprite)",
      "price": 2.50,
      "quantity": 1
    }
  ],
  "total": "11.50"
}
```

#### 3. Combo Deal Order ⭐ **NEW**:
```json
{
  "deliveryType": "collection",
  "customer": {
    "fullName": "Alice Brown",
    "phone": "555-9876",
    "email": "alice@example.com"
  },
  "items": [
    {
      "name": "Bird's Feast Combo [Combo Deal]",
      "price": 18.50,
      "quantity": 1,
      "isCombo": true,
      "comboItems": [
        {
          "name": "Classic Hot Tenders",
          "quantity": 1,
          "includedInCombo": true
        },
        {
          "name": "Chicken Tenders or Wings",
          "option": "10 piece",
          "quantity": 1,
          "includedInCombo": true
        },
        {
          "name": "Fries",
          "quantity": 2,
          "includedInCombo": true
        },
        {
          "name": "Pepsi",
          "quantity": 2,
          "includedInCombo": true
        }
      ]
    }
  ],
  "total": "18.50"
}
```

**Key points for backend:**

* `selectedOption` can be a variant name (Chicken/Lamb) or portion size (10 piece). It comes directly from the JSON `options[].name`.
* `price` is always per-unit price from the chosen option (or base price if no options).
* If chips/drink is added, you'll always see a second line `{ "name": "Chips & Drink (DrinkName)", "price": mealPriceModifier, "quantity": sameAsMainItem }`.
* If no chips/drink, there's no second line.
* Sauces/vegetables are only on the main line.
* **Combo Deals** ⭐ **NEW**: Include `isCombo: true` and `comboItems` array with all included items for kitchen reference.

---

## 8. New Categories Overview ⭐ **NEW**

### Hot Tenders Category
- Regular menu items (individual pricing)
- Can be added to combo deals
- Support sauce selection
- Meal upgrades available

### Hot Deals Category (Combo Deals)
- **Bundled pricing** (not sum of individual items)
- Show included items when clicked in modal
- **Receipt indication**: `[Combo Deal]` suffix
- **Backend payload**: Includes all combo items for kitchen reference
- No meal upgrades (already complete meals)

---

## 9. Backups & Support

* Always **keep a backup** of JSON files before making changes.
* If something breaks, restore the previous backup.
* Use the **JSON Converter Tool** to avoid syntax errors.
* The Developer can provide guidance if needed, but **ongoing menu management is the Client's responsibility**.

---

## 10. Deploying Changes to Vercel

The site is automatically deployed from this GitHub repository using Vercel.

* **If you edit files directly on GitHub**
  Save/commit your changes. Vercel will automatically pick up the new commit and redeploy within a minute or two.

* **If you work locally on your PC**
  1. Pull or clone the repo.
  2. Make your JSON/image changes.
  3. Commit and push to the `main` branch (or the branch Vercel is connected to).

  Vercel will build and deploy automatically after your push.

* **Check deployment status**
  In your Vercel dashboard you'll see the deployment logs and the new version going live.

---

## 11. API Integration (Future-Proofing)

The front-end code is already set up to talk to a backend API when it becomes available:

```js
// In index.html
const API_BASE = ''; // e.g. 'https://api.yoursite.com'

// Helper to get file/API URL
function getJsonUrl(file) {
  return API_BASE ? `${API_BASE}/${file}` : file;
}
```

* **Current behaviour**: With `API_BASE = ''` the site loads the JSON files locally and does not send orders anywhere.
* **When backend is ready**: Set `API_BASE` to your API's URL (for example `https://api.hotbird.com`).

  * Menu JSON will be fetched from the API instead of local files.
  * Orders will automatically be sent to `${API_BASE}/orders` via `POST`.

No other code changes are needed — just update the `API_BASE` value.

---

## Quick Reference

* **JSON Converter Tool:** [https://json-convertor-hot-bird.vercel.app](https://json-convertor-hot-bird.vercel.app)
* **Image Size:** 1200×1200 px
* **Image Folder:** `images/`
* **Special Tags:** 
  - `"D"` for drinks
  - `"M"` for milkshakes  
  - `"combo"` for combo deals
* **New Categories:** `hottenders`, `hotdeals`
* **Meal Upgrade:** Use `mealPriceModifier` field
* **Combo Items:** Use `comboItems` array for bundled deals
* **Validation:** Always test JSON at [jsonlint.com](https://jsonlint.com) or use our converter tool
```

## Key Updates Made:

1. **Added New JSON Files**: Added `hot-tenders.json` and `hot-deals.json` to the file list
2. **New Category Examples**: Added comprehensive examples for Hot Tenders and Combo Deals
3. **Combo Items Field**: Documented the new `comboItems` array structure
4. **Updated Order Payloads**: Added combo deal order example for backend
5. **Category Overview**: Added section explaining the two new categories
6. **Special Tags**: Added `"combo"` tag documentation
7. **Quick Reference**: Updated with new categories and features
8. **Visual Indicators**: Used ⭐ **NEW** markers to highlight recent additions

The README now fully documents the new Hot Tenders and Hot Deals functionality while maintaining all existing documentation.
