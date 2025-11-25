# Playwright 

Este repositorio contiene una suite de tests E2E usando Playwright + TypeScript para la aplicación OpenSource OrangeHRM (demo).

**Propósito:**
- Proveer ejemplos de Page Objects, tests, y reportes (HTML, JUnit, Allure).

**Estructura principal del repositorio**
- `playwright.config.ts` — Configuración de Playwright (proyectos, reporter, timeouts).
- `tests/` — Tests y Page Objects.
  - `tests/pages/` — Clases de Page Object (`SuperPage.ts`, `LoginPage.ts`, `AddSystemUserPage.ts`).
  - `tests/e2e/` — Tests E2E (`login.test.ts`, `addUserCredentials.test.ts`).
  - `tests/custom-reporter.ts` — Reporter personalizado.
- `test-results/`, `test-html-report/`, `test-junit-report/`, `allure-results/` — Salida de reportes y artefactos.

Requisitos (local):
- Node.js (recomendado >= 18)
- npm (incluido con Node.js)

Instalación de dependencias:
```bash
npm install
# Si aún no has instalado navegadores de Playwright:
npx playwright install
```

Variables de entorno
--------------------
La suite espera credenciales para login en variables de entorno. Crea un archivo `.env` en la raíz del proyecto con las siguientes claves:

```
ORANGE_USERNAME=Admin
ORANGE_PASSWORD=admin123
```

Asegúrate de usar las credenciales correctas para el entorno de prueba.

Ejecutar tests
---------------
Ejecutar todos los tests:

```bash
npx playwright test
```

Ejecutar un test específico (por ruta):

```bash
npx playwright test tests/e2e/login.test.ts
```

Ver más salida en consola (reporter line):

```bash
npx playwright test --reporter=line
```

Reportes
--------
- HTML: `test-html-report/` (configurado en `playwright.config.ts`). Para abrir el reporte generado:

```bash
npx playwright show-report
```

- Allure: los resultados se escriben en `allure-results/`. Para generar el reporte y abrirlo (si tienes `allure-commandline` instalado):

```bash
npx allure generate --clean allure-results -o allure-report
npx allure open allure-report
```

Notas importantes y solución de problemas
----------------------------------------
- Error común "Missing CREDENTILAS in ENV VARS": significa que faltan `ORANGE_USERNAME` o `ORANGE_PASSWORD` en el entorno. Crea/actualiza `.env` y reintenta.
- Si los selectores fallan por cambios en la UI, revisa los Page Objects en `tests/pages/` y actualiza los selectores.
- Para reproducir fallos con trazas y capturas: Playwright guarda `trace.zip` y screenshots en `test-results/` cuando un test falla.

Consejos adicionales
-------------------
- Mantén `playwright.config.ts` sincronizado con tus necesidades de CI (workers, retries).
- Agrega `script` en `package.json` para comandos comunes, por ejemplo:
```json
"scripts": {
  "test": "playwright test",
  "test:report": "playwright show-report"
}
```