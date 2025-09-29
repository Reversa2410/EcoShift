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
      int id PK
      string full_name
      string email
      string phone
      string role
      string plan_code
      datetime created_at
      datetime updated_at
    }

    PLANS {
      int id PK
      string code
      int monthly_photo_limit
      float price_usd
      boolean is_active
      datetime created_at
      datetime updated_at
    }

    SUBSCRIPTIONS {
      int id PK
      int user_id FK
      int plan_id FK
      datetime start_date
      datetime end_date
      string status
      string provider
      string provider_ref
      datetime created_at
      datetime updated_at
    }

    PHOTOS {
      int id PK
      int user_id FK
      string storage_path
      string source
      datetime taken_at
      datetime uploaded_at
    }

    ANALYSES {
      int id PK
      int photo_id FK
      int user_id FK
      int condition_id FK
      float confidence
      string status
      string advice_summary
      datetime created_at
    }

    CONDITIONS {
      int id PK
      string code
      string name
      string type
      string crop
      string severity_scale
      string description
    }

    RECOMMENDATIONS {
      int id PK
      int condition_id FK
      string title
      string body
      string category
      string region
      boolean active
    }

    USAGE_LOGS {
      int id PK
      int user_id FK
      string action
      int quantity
      datetime occurred_at
    }


