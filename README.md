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

⚠️ **Important:** All JSON files must be located in the same directory as `index.html`.
Images for menu items are stored in the `images/` folder, so the `image` field should point to `images/YourImageName.jpg`.

---

## 2. Understanding a Menu Item JSON Object

Example:

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
* **mealPriceModifier**: Extra cost when upgrading to a meal. *(decimal)*
* **options** *(optional)*: Variations of the item.
  * **Special behavior:**
    * If *all options* have prices → price shows on the **button**.
    * If *not all options* have prices → price shows in the **dropdown**.
* **showSlider**: Always set to `false` (legacy field).
* **sauces**: `true`/`false` – whether customer can choose sauces.
* **vegetables**: `true`/`false` – whether customer can choose vegetables.

---

## 3. Image Rules

* **Size**: All images must be **1200 × 1200 px**.
* **Format**: `.jpg` or `.png`.
* **Location**: All images go inside the `images/` folder.
* **Naming**: Must match exactly the `image` field in JSON (case-sensitive), including the `images/` prefix.

**Special Cases:**

* **Drinks** (`"D"` tag): Canned drinks centered properly.
* **Milkshakes** (`"M"` tag): Full image always shown, scaled outward.
* **All Other Items**: Positioned according to Website Manager's preferences.

---

## 4. Editing Workflow

1. Identify which JSON file contains the category.
2. Copy an existing item as a template.
3. Edit `name`, `description`, `image`, `tags`, `price/options`.
4. Save the JSON file.
5. Add the image file (1200×1200 px) to the `images/` folder.
6. **Use the JSON Converter Tool** (see below) to validate and format your JSON.
7. Refresh the website to see changes.

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

---

## 7. Order Payload Examples for Backend

These show how the front-end sends orders to the backend with different combinations:

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

#### 3. Samosas (Chicken) with Chips & Drink:

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
      "name": "Samosas (3 Pieces) (Chicken)",
      "price": 2.50,
      "quantity": 1,
      "selectedOption": "Chicken"
    },
    {
      "name": "Chips & Drink (Pepsi)",
      "price": 2.50,
      "quantity": 1
    }
  ],
  "total": "5.00"
}
```

**Key points for backend:**

* `selectedOption` can be a variant name (Chicken/Lamb) or portion size (10 piece). It comes directly from the JSON `options[].name`.
* `price` is always per-unit price from the chosen option (or base price if no options).
* If chips/drink is added, you'll always see a second line `{ "name": "Chips & Drink (DrinkName)", "price": mealPriceModifier, "quantity": sameAsMainItem }`.
* If no chips/drink, there's no second line.
* Sauces/vegetables are only on the main line.

---

## 8. Backups & Support

* Always **keep a backup** of JSON files before making changes.
* If something breaks, restore the previous backup.
* Use the **JSON Converter Tool** to avoid syntax errors.
* The Developer can provide guidance if needed, but **ongoing menu management is the Client's responsibility**.

---

## 9. Deploying Changes to Vercel

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

## 10. API Integration (Future-Proofing)

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
* **Special Tags:** `"D"` for drinks, `"M"` for milkshakes
* **Meal Upgrade:** Use `mealPriceModifier` field
* **Validation:** Always test JSON at [jsonlint.com](https://jsonlint.com) or use our converter tool
