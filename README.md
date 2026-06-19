# Puentes de Papel 🌉📄

**Puentes de Papel** es una iniciativa de **Munay Ruray** diseñada para conectar generaciones a través de historias y memorias. La plataforma une a jóvenes voluntarios con personas mayores para compartir historias de vida, rescatar memorias y generar vínculos significativos.

Este sitio web está construido utilizando [Astro](https://astro.build/) y estilizado con [Tailwind CSS](https://tailwindcss.com/) y [Lucide Icons](https://lucide.dev/).

---

## 🛠️ Tecnologías y Requisitos

*   **Entorno:** [Bun](https://bun.sh/) (recomendado) o Node.js v22.12.0 o superior.
*   **Framework:** Astro v6.
*   **Estilos:** Tailwind CSS v4.

---

## 🚀 Inicio Rápido

1.  **Instalar dependencias:**
    ```bash
    bun install
    ```

2.  **Configurar variables de entorno:**
    Crea un archivo `.env` en la raíz del proyecto basándote en el archivo de plantilla `.env.example`:
    ```bash
    cp .env.example .env
    ```
    *(Ver detalles de configuración más abajo)*.

3.  **Correr en modo de desarrollo:**
    ```bash
    bun dev
    ```
    El servidor local se abrirá en `http://localhost:4321`.

4.  **Compilar para producción:**
    ```bash
    bun build
    ```
    El resultado estático se generará en la carpeta `dist/` listo para ser desplegado.

---

## ⚙️ Variables de Entorno (`.env`)

El sitio web utiliza variables de entorno nativas de Astro para manejar integraciones y el progreso de la campaña de donaciones sin exponer datos sensibles.

| Variable | Descripción | Ejemplo / Valor por defecto |
| :--- | :--- | :--- |
| `PUBLIC_APPS_SCRIPT_URL` | Endpoint de Google Apps Script encargado de capturar y guardar los envíos de formularios en Google Sheets (Voluntarios, Residencias y Adultos Mayores). | `https://script.google.com/macros/s/.../exec` |
| `PUBLIC_DONATION_URL` | Enlace al perfil de **Cafecito.app** del cliente (para donar mediante Mercado Pago). | `https://cafecito.app/tu_usuario` |
| `PUBLIC_CURRENT_RAISED` | Monto recaudado acumulado en la campaña (suma de transferencias + Cafecito). | `0` |
| `PUBLIC_TARGET_GOAL` | Meta total de recaudación de la campaña en pesos argentinos. | `10000000` |

### 💡 Comportamiento Inteligente de Donaciones
*   **Si `PUBLIC_DONATION_URL` está configurado:** Al hacer clic en *"Quiero colaborar"* o *"Quiero ser embajador/a"*, el sitio web redirigirá automáticamente a la pasarela de Cafecito en una pestaña nueva.
*   **Si `PUBLIC_DONATION_URL` se deja vacío:** Al hacer clic en los botones de donación, el sitio web realizará un **desplazamiento suave (smooth scroll)** directamente hasta la sección de **datos de transferencia bancaria (CBU / Alias)**. Esto permite que el sitio siga siendo plenamente funcional aunque aún no se tenga o no se desee usar la pasarela digital.

### 📈 Cómo Actualizar el Progreso de la Campaña
Dado que es un sitio estático súper veloz, el monto recaudado se define en tiempo de compilación. Para actualizar el indicador de progreso:
1. Revisa el balance total (Brubank + Cafecito).
2. Modifica la variable `PUBLIC_CURRENT_RAISED` en tu archivo `.env` local o en el panel de control de tu proveedor de hosting (ej. Vercel, Netlify, Cloudflare).
3. Guarda los cambios para gatillar un re-despliegue de la web (toma menos de 1 minuto).

---

## 📁 Estructura del Proyecto

```text
/
├── public/              # Archivos estáticos (imágenes, fuentes, favicons)
├── src/
│   ├── components/      # Componentes reutilizables de Astro (Layouts, etc.)
│   ├── pages/           # Páginas del sitio (rutas automáticas de Astro)
│   │   ├── index.astro            # Página principal / Campaña
│   │   ├── voluntarios.astro      # Formulario de voluntarios
│   │   ├── residencias.astro      # Formulario de residencias
│   │   └── adultos-mayores.astro  # Formulario de adultos mayores
│   └── styles/          # Estilos globales CSS
├── .env.example         # Plantilla de variables de entorno
├── astro.config.mjs     # Configuración del proyecto Astro
└── package.json         # Dependencias y scripts
```
