# 🌱 EcoShift

EcoShift es una aplicación móvil desarrollada en **Flutter** que ayuda a los agricultores nicaragüenses de frijol a detectar plagas y enfermedades en sus cultivos mediante el uso de **modelos de Inteligencia Artificial**.  
El objetivo principal es empoderar a los agricultores con una herramienta accesible, práctica y confiable para mejorar la salud de sus cultivos y garantizar la seguridad alimentaria.

---

## 🚀 Características
- Subir fotos de plantas de frijol desde la cámara o galería.
- Diagnóstico preliminar de plagas o enfermedades mediante IA.
- Recomendaciones prácticas para el cuidado y tratamiento del cultivo.
- Interfaz sencilla y amigable para agricultores con baja experiencia tecnológica.
- Versión gratuita con límite de fotos y planes premium para uso extendido.

  ## ⚙️ Funcionalidades implementadas
- Captura de foto con la cámara.
- Subida de imágenes desde la galería.
- Interfaz de resultados con diagnóstico simulado.
- Limitación de fotos en el plan gratuito.
- Navegación básica entre pantallas.


---

## 📋 Requisitos Previos
- [Flutter SDK](https://docs.flutter.dev/get-started/install) (versión 3.0 o superior).
- Dart SDK.
- Android Studio o Visual Studio Code con las extensiones de Flutter y Dart.
- Un dispositivo Android o emulador configurado.

---

## 🔧 Instalación y Ejecución
1. Clona este repositorio:
   ```bash
   git clone https://github.com/usuario/ecoshift.git
   cd ecoshift

## 🗂️ Diagramación de la Base de Datos

```mermaid
erDiagram
    USERS ||--o{ PHOTOS : "toma"
    USERS ||--o{ ANALYSES : "recibe"
    USERS }o--|| PLANS : "tiene"
    USERS ||--o{ SUBSCRIPTIONS : "se_suscribe"
    PHOTOS ||--|| ANALYSES : "analiza"
    ANALYSES }o--|| CONDITIONS : "detecta"
    CONDITIONS ||--o{ RECOMMENDATIONS : "sugiere"
    USERS ||--o{ USAGE_LOGS : "registra"

    USERS {
      uuid id PK
      text full_name
      text email
      text phone
      text role "farmer|tech|admin"
      text plan_code "FREE|BASIC|PRO"
      timestamptz created_at
      timestamptz updated_at
    }

    PLANS {
      uuid id PK
      text code "FREE|BASIC|PRO" UNIQUE
      int monthly_photo_limit
      numeric price_usd
      boolean is_active
      jsonb features
      timestamptz created_at
      timestamptz updated_at
    }

    SUBSCRIPTIONS {
      uuid id PK
      uuid user_id FK
      uuid plan_id FK
      timestamptz start_date
      timestamptz end_date
      text status "active|past_due|canceled|expired"
      text provider "stripe|internal"
      text provider_ref
      timestamptz created_at
      timestamptz updated_at
    }

    PHOTOS {
      uuid id PK
      uuid user_id FK
      text storage_path
      text source "camera|gallery"
      text note
      timestamptz taken_at
      timestamptz uploaded_at
    }

    ANALYSES {
      uuid id PK
      uuid photo_id FK UNIQUE
      uuid user_id FK
      uuid condition_id FK
      numeric confidence "0.000–1.000"
      text status "ok|failed|pending"
      text advice_summary
      jsonb model_meta
      timestamptz created_at
    }

    CONDITIONS {
      uuid id PK
      text code UNIQUE
      text name
      text type "disease|pest|deficiency"
      text crop "bean"
      text severity_scale "low|med|high"
      text description
    }

    RECOMMENDATIONS {
      uuid id PK
      uuid condition_id FK
      text title
      text body
      text category "cultural|biologic|chemical|irrigation"
      text region "NI|CA|GLOBAL"
      jsonb safety_notes
      boolean active
    }

    USAGE_LOGS {
      uuid id PK
      uuid user_id FK
      text action "photo_analyzed"
      int quantity
      timestamptz occurred_at
      jsonb meta
    }


