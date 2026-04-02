You will receive unstructured data blocks describing fantasy items (weapons, relics, artifacts, etc). Your task is to **normalize ALL data into a strict, consistent JSON format**, following the schema below.

## 📌 GLOBAL RULES

* Output **ONLY valid JSON**
* ALL field names AND values MUST be in **ENGLISH**
* Translate any non-English content to English
* Normalize ALL items to the same structure
* NEVER omit fields — all fields must exist
* If data is missing:

    * use `0` for numbers
    * use `""` for strings
    * use `[]` for arrays
* Interpret narrative descriptions into structured data
* You may **infer reasonable values** when needed
* If new types of data appear, **incorporate them without breaking the structure**, using:

    * `modifiers`
    * `special_effects`
    * `tags`
    * or semantically expanding existing fields

---

## 🧱 REQUIRED SCHEMA

```json
{
  "id": "string",
  "name": "string",

  "category": "weapon | relic | artifact | accessory",
  "subtype": "staff | wand | sword | orb | totem | bow | slingshot | other",

  "rarity": "common | uncommon | rare | epic | legendary | mythic | unique | divine",

  "primary_class": "string",
  "tags": ["string"],

  "description": "string",
  "expanded_lore": "string",

  "status": {
    "attack": 0,
    "defense": 0,
    "magic": 0,
    "support": 0,
    "mobility": 0,
    "control": 0
  },

  "attributes": {
    "strength": 0,
    "dexterity": 0,
    "intelligence": 0,
    "vitality": 0,
    "spirit": 0,
    "luck": 0
  },

  "modifiers": [
    {
      "type": "damage | defense | healing | crit | speed | utility",
      "value": 0,
      "unit": "flat | percent",
      "condition": "string"
    }
  ],

  "passives": [
    {
      "name": "string",
      "effect": "string",
      "condition": "string"
    }
  ],

  "abilities": [
    {
      "name": "string",
      "type": "active | ultimate",
      "effect": "string",
      "cooldown": 0,
      "cooldown_unit": "s | min | h | none"
    }
  ],

  "special_effects": ["string"],
  "restrictions": ["string"],

  "origin": {
    "type": "natural | forged | divine | unknown",
    "location": "string"
  },

  "meta": {
    "instagram_id": "string"
  }
}
```

---

## 🔄 NORMALIZATION RULES

* Star ratings (★★★★★) → numeric values (e.g. 5)
* Percent values → `value` + `"percent"`
* Direct values → `"flat"`
* Convert vague text into:

    * `effect`
    * `condition`
* Cooldowns must be numeric + separate unit
* Always separate:

    * passives ≠ abilities
* Convert any bonuses into `modifiers` whenever possible

---

## 🧠 INTERPRETATION RULES

* Correctly classify:

    * `category`
    * `subtype`
    * `rarity`
* Extract as much structured data as possible
* If something is too unique → use `special_effects`
* If there are costs, risks, or limitations → use `restrictions`

---

## 📥 INPUT

(paste the raw data blocks here)