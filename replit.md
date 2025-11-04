# Overview

InBack/Clickback is a Flask-based real estate platform specializing in cashback services for new construction properties in the Krasnodar region. It connects buyers and developers, offers property listings, streamlines application processes, and integrates CRM tools. The platform aims to provide unique cashback incentives, an intuitive user experience, intelligent property search with interactive maps, residential complex comparisons, user favorites, a manager dashboard for client and cashback tracking, and robust notification and document generation capabilities. The project is currently expanding to support multiple cities across Krasnodarsky Krai and the Republic of Adygea.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend

The frontend uses server-side rendered HTML with Jinja2 and CDN-based TailwindCSS for a mobile-first, responsive design. Interactivity is managed by modular vanilla JavaScript, including smart search, real-time filtering, Yandex Maps integration, property comparison, and PDF generation.

## Backend

Built with Flask 2.3.3, the backend employs an MVC pattern with blueprints. SQLAlchemy with PostgreSQL serves as the ORM. Key features include Flask-Login for session management and RBAC (Regular Users, Managers, Admins), robust security, and custom parsing for Russian address formats. The system supports phone verification and manager-to-client presentation delivery. Data is structured using normalized Developers → Residential Complexes → Properties schemas and a Repository Pattern for data access. The system supports multi-city data management, dynamic city selection, and city-aware data filtering.

## Data Storage

PostgreSQL, managed via SQLAlchemy 2.0.32, is the primary database. The schema includes Users, Managers, Properties, Residential Complexes, Developers, Marketing Materials, transactional records, and search analytics. Flask-Caching optimizes performance. `residential_complexes` includes rich content fields and a `complex_type` field. `marketing_materials` stores promotional content linked to residential complexes.

## Authentication & Authorization

The system supports Regular Users, Managers, and Admins through a unified Flask-Login system with dynamic user model loading.

## Intelligent Address Parsing & Search System

This system leverages DaData.ru for address normalization and Yandex Maps Geocoder API for geocoding. It features auto-enrichment for new properties, optimized batch processing, smart caching, and city-aware address suggestions. The database schema supports granular search and filtering.

## UI/UX and Feature Specifications

-   **AJAX-powered Sorting and Filtering:** Property listings feature an AJAX API for fast, scalable sorting and filtering, with infinite scroll and view mode persistence.
-   **Residential Complex Image Sliders:** Multi-photo sliders with fallback.
-   **Comparison System:** PostgreSQL-backed comparison for properties and complexes with strict limits.
-   **Interactive Map Pages:** Full-height Leaflet and Yandex Maps display residential complexes and properties with color-coded markers, grouping, server-side filtering, sticky search/filter bars, and mobile-optimized bottom sheets.
-   **Unified Filter + Search Row (Desktop):** Consistent desktop design for `/residential-complexes` and `/properties` pages, combining filters and search in a single horizontal row with SuperSearch suggestions and filter badge counters.
-   **Mobile Sticky Search Bar:** Avito-style compact sticky search bar with backdrop blur, bidirectional search input sync, and integrated controls. Features include fullscreen filter overlays with real-time object counters and advanced filters.
-   **Fullscreen Map Modals (Mobile):** Interactive Yandex Maps modals for complexes and properties, with compact filter toolbars, bottom sheet quick filters, and advanced filter modals.
-   **Saved Search Feature:** Fullscreen mobile modal for saving property searches, with authentication checks, filter previews, and smart search name generation.
-   **Smart Search with Database-Backed History:** Real-time suggestions via SuperSearch, supporting flexible query formats and tracking for analytics.
-   **Dynamic Results Counter:** Updates property count with correct Russian declension.
-   **Property Alert Notification System:** Comprehensive system for saved searches with instant, daily, and weekly alerts via email and Telegram, configurable frequency, delivery channels, and one-click unsubscribe.
-   **Marketing Materials Management:** Comprehensive management system for residential complex marketing materials, including database storage, admin panel CRUD, quick-add functionality, and file validation.
-   **Action Buttons on Detail Pages:** User-facing "Favorite," "Compare," and "Share" buttons on property and residential complex detail pages.
-   **Excursion/Online Showing CTA Blocks:** Conversion-focused call-to-action blocks on complex and property detail pages respectively, integrating with application modals.
-   **City Selector UI:** Dynamic city selection and persistence across the platform with correct Russian grammar declensions.
-   **Automatic City Detection:** Detects user's city via IP and sets it in the session for localized content.

# External Dependencies

## Third-Party APIs

-   **SendGrid**: Email sending.
-   **OpenAI**: Smart search and content generation.
-   **Telegram Bot API**: User notifications and communication.
-   **Yandex Maps API**: Interactive maps, geocoding, and location visualization.
-   **DaData.ru**: Address normalization, suggestions, and geocoding.
-   **SMS.ru, SMSC.ru**: Russian SMS services for phone verification.
-   **Google Analytics**: User behavior tracking.
-   **LaunchDarkly**: Feature flagging.
-   **Chaport**: Chat widget.
-   **reCAPTCHA**: Spam and bot prevention.
-   **ipwho.is**: IP-based city detection.

## Web Scraping Infrastructure

-   `selenium`, `playwright`, `beautifulsoup4`, `undetected-chromedriver`: Used for automated data collection.

## PDF Generation

-   `weasyprint`, `reportlab`: Used for generating property detail sheets, comparison reports, and cashback calculations.

## Image Processing

-   `Pillow`: Used for image resizing, compression, WebP conversion, and QR code generation.