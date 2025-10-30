# Mintlify Documentation Setup

Esta carpeta contiene todos los archivos necesarios para crear el repositorio de documentación con Mintlify.

## Archivos Incluidos

- `mint.json` - Configuración principal de Mintlify
- `introduction.mdx` - Página de introducción
- `authentication.mdx` - Documentación de autenticación
- `quickstart.mdx` - Guía de inicio rápido
- `api-reference.mdx` - Referencia de API (usa OpenAPI)
- `.github/workflows/sync-openapi.yml` - Workflow para sincronizar OpenAPI automáticamente

## Pasos para Configurar

### 1. Crear el Repositorio de Mintlify

```bash
# Opción A: Usar el starter de Mintlify
npx create-mint@latest relayer-docs
cd relayer-docs

# Opción B: Crear manualmente
mkdir relayer-docs
cd relayer-docs
git init
```

### 2. Copiar Archivos

Copia todos los archivos de esta carpeta `mintlify/` al nuevo repositorio:

```bash
# Desde el repositorio de Mintlify
cp -r /path/to/sherry-api/mintlify/* .
```

### 3. Configurar el Workflow

Edita `.github/workflows/sync-openapi.yml` y reemplaza `tu-org/sherry-api` con el nombre real de tu repositorio:

```yaml
API_REPO: ${{ github.event.inputs.api_repo || 'tu-organizacion/relayer-api' }}
```

### 4. Descargar OpenAPI Inicial

Descarga el archivo OpenAPI inicial:

```bash
curl -L "https://raw.githubusercontent.com/tu-org/relayer-api/main/docs/openapi.json" -o openapi.json
```

### 5. Configurar Mintlify

1. Ve a [mintlify.com](https://mintlify.com)
2. Crea una cuenta o inicia sesión
3. Crea un nuevo proyecto
4. Conecta tu repositorio de GitHub (relayer-docs)
5. Mintlify detectará automáticamente `mint.json`

### 6. Personalizar

- Actualiza los links en `mint.json` (logo, favicon, redes sociales)
- Añade más páginas según necesites
- Personaliza colores y branding

## Sincronización Automática

El workflow `sync-openapi.yml` se ejecutará:
- Automáticamente cada hora para verificar actualizaciones
- Manualmente usando `workflow_dispatch`

Cuando detecte cambios en el OpenAPI, hará commit automático y Mintlify desplegará automáticamente.

## Notas

- El archivo `openapi.json` debe estar en la raíz del repositorio de Mintlify
- Asegúrate de que el workflow tenga permisos de escritura en GitHub
- Los cambios en `mint.json` y páginas MDX también triggeran deploy automático en Mintlify
