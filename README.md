# Shopify Multi-Store Build: 5 Branded Fashion Stores from One Catalogue

> **Case study.** This repository documents the approach and results only. The theme code, store data and automation scripts are private and are not included.

## Overview

I built five separate leather-jacket stores on Shopify from one shared catalogue of **1,799 products**. Each store has its own brand, design and wording, but runs on the same proven structure:

| Brand | Role |
|---|---|
| Rowan & Hide | First store: built and tuned by hand |
| Ashford & Co. | Rollout store |
| Marlowe & Stone | Rollout store |
| Hartwell & Gray | Rollout store |
| Rook & Ridge | Rollout store |

The first store, Rowan & Hide, was built and tuned by hand. The other four reuse its structure, so each one could be set up in hours instead of days.

## What each store gets

### 1. Navigation that matches how people shop
- A mega menu: **MEN · WOMEN · SUITS & TUX · STYLES · BRAND & SUPPORT · DEALS**
- Footer menus for Customer Care, Information and Shop by Style
- The same menu layout in every store, so analytics and ads can be compared across brands

### 2. 47 smart collections per store
- **By product type:** leather, blazers, coats, suits, satin, denim, cotton, wool, fleece, puffer, hoodies, tracksuits, vests
- **By style:** bomber, biker, cafe racer, vintage, shearling, varsity, hooded, slim fit, winter
- **By colour:** black, brown, red, white, blue
- **Deals:** New Arrivals, Best Sellers, Mega Deals (any product with a reduced price)
- **Men's and women's lines:** a full set of women's collections (jackets, coats, blazers, bomber, biker, hooded, varsity, black, brown)

All collections are rule-based, so new products drop into the right place on import without manual sorting.

### 3. Men / Women split from messy product data
The imported catalogue had no gender field. Gender was hidden in each product's **size option name** ("Women Sizes", "Men Sizes", "Select Gender").

- I exported all 1,799 products, read every product's option names and tagged each one `Men`, `Women` or both
- Result per store: **1,187 men's** and **841 women's** products (229 unisex products appear in both)
- The MEN and WOMEN menus are built from those tags, so they never mix

### 4. Unique content per brand
- 11 store pages per brand: Our Story, Contact, FAQs, Returns & Exchanges, Shipping, Payment, Order Cancellation, Terms, Privacy, Track Your Order, Customer Reviews
- Each brand has **its own wording**, not copy-paste, to avoid duplicate-content issues between the stores
- Collection descriptions are rewritten per brand as well

### 5. Apps and product page
- **Judge.me** review stars and widget
- **BF Size Charts** on every product page
- Custom CSS so the size chart image keeps its real proportions instead of stretching to the popup width
- Trust badges, shipping and returns info, and a sticky add-to-cart bar

## How the rollout works

```
Brand theme zip  ──►  Install apps  ──►  Upload theme  ──►  Import catalogue
                                                              │
        ┌─────────────────────────────────────────────────────┘
        ▼
Build collections (47) ─► Tag Men/Women (1,799) ─► Create pages (11) ─► Build menus (4)
        │
        ▼
Restore app blocks on a draft theme ─► Verify file checksums ─► Owner publishes
```

Everything was done through the **Shopify Admin GraphQL API**:

- Smart collections created and published in batches
- Product tags written in batches of 100
- Pages and menus created from templates that hold each brand's wording
- Theme changes made only on **draft copies**. The live theme is never edited directly; the owner reviews and publishes.

## Problems solved along the way

| Problem | Fix |
|---|---|
| Shopify strips app blocks from an uploaded theme if the apps aren't installed yet | Restored the review stars and size chart blocks from the original templates on a draft theme |
| Shopify overwrote edits made while a duplicated theme was still processing | Wait for processing to finish, then upload and verify each file's checksum |
| Bulk tag updates are blocked through the connector | Wrote tags in batched API calls of 100 instead |
| Size chart image stretched to the popup width | CSS that keeps the image's own aspect ratio |
| Template placeholder email on every product page | Replaced with the real support address in the theme package itself |

## Results

- **5 stores** on one shared structure
- **188 collections** across the four rollout stores (47 each), all published
- **44 pages** across the four rollout stores (11 each), each in the brand's own wording
- **7,196 products** tagged Men/Women across the four rollout stores, none missed
- Every new store is now set up in **one session** from a reusable process

## Tech

Shopify (Online Store 2.0, Liquid) · Shopify Admin GraphQL API · Node.js for batch generation · Judge.me · BF Size Charts

## Related

Speed work on the same stores: [shopify-speed-optimization](https://github.com/FawadCyber/shopify-speed-optimization)

---

© Fawad Naseem. Case study only; no source code is published. All rights reserved.
