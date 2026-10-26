# Configuración de Visual Studio Code

Documentación de la configuración de VS Code usada en este workspace (**Arquitectura de Microservicios**).

- Configuración de usuario: `%APPDATA%\Code\User\settings.json`
- Configuración del workspace: `.vscode\settings.json` y `.vscode\launch.json`

---

## 1. Apariencia

| Ajuste | Valor |
|---|---|
| Tema de color | Tokyo Night |
| Tema de iconos | Material Icon Theme |
| Idioma | Español (paquete de idioma instalado) |
| Minimap | Desactivado |
| Barra lateral secundaria | Oculta por defecto |
| Reglas verticales | Columnas 80 (verde), 100 (amarillo), 120 (salmón), muy tenues |

**Personalización de colores (`workbench.colorCustomizations`):**

- Tema *Default Dark Modern*: borde superior verde en la pestaña activa.
- Resaltado de palabra: borde dorado (`#FFD700`) y rojo tomate (`#FF6347`) para escrituras.
- Resaltado de selección: borde gris (`#A9A9A9`).

## 2. Edición

| Ajuste | Valor | Efecto |
|---|---|---|
| `files.eol` | `\n` | Fin de línea LF. Los archivos `.bat` usan `\r\n`. |
| `editor.linkedEditing` | `true` | Editar una etiqueta HTML edita también su par. |
| `editor.unicodeHighlight.includeComments` | `true` | Resalta caracteres Unicode sospechosos también en comentarios. |
| `workbench.editor.revealIfOpen` | `true` | Si un archivo ya está abierto, enfoca esa pestaña. |
| `explorer.confirmDelete` | `false` | No pide confirmación al borrar archivos. |
| `emmet.variables.lang` | `es` | Idioma por defecto en plantillas Emmet. |
| `cSpell.diagnosticLevel` | `Hint` | Los errores ortográficos se muestran solo como sugerencia. |
| `trailing-spaces` | Fondo rojo tenue, sin líneas vacías | Marca espacios sobrantes al final de línea. |

## 3. Java

### JDKs configurados

| Nombre | Ruta |
|---|---|
| JavaSE-11 | `C:\Program Files\Java\jdk-11` |
| JavaSE-17 | `C:\Program Files\Java\jdk-17.0.0.1` |
| JavaSE-21 | `C:\Program Files\Eclipse Adoptium\jdk-21.0.11.10-hotspot` |
| JavaSE-25 | `...\globalStorage\pleiades.java-extension-pack-jdk\java\25` |
| JavaSE-26 (**por defecto**) | `...\globalStorage\pleiades.java-extension-pack-jdk\java\latest` |

### Ajustes del lenguaje

- `java.configuration.updateBuildConfiguration`: `automatic` (usuario) / `interactive` (workspace, es el que aplica aquí).
- `java.compile.nullAnalysis.mode`: `automatic`.
- `java.configuration.detectJdksAtStart`: `false`.
- `java.debug.settings.hotCodeReplace`: `auto`.
- `java.debug.settings.onBuildFailureProceed`: `true` (workspace).
- `java.maxConcurrentBuilds`: `8`.
- `java.dependency.packagePresentation`: `hierarchical`.
- `java.sources.organizeImports.staticStarThreshold`: `1`.
- `java.test.config.vmArgs`: `-Dstdout.encoding=UTF-8 -Dstderr.encoding=UTF-8`.

### Maven y Gradle

Usan las versiones `latest` incluidas en el Pleiades Java Extension Pack:

- `maven.executable.path` → `...\pleiades.java-extension-pack-jdk\maven\latest\bin\mvn`
- `java.import.gradle.home` → `...\pleiades.java-extension-pack-jdk\gradle\latest`
- `java.import.gradle.java.home` y `maven.terminal.customEnv` (`JAVA_HOME`) → JDK 25.

## 4. Terminal

- **Perfil por defecto:** `JavaSE-26`.
- **Perfiles disponibles (cmd):** `JavaSE-11 LTS`, `JavaSE-17 LTS`, `JavaSE-21 LTS`, `JavaSE-25 LTS`, `JavaSE-26`.
  - Cada uno define `JAVA_HOME` y antepone su `bin` al `PATH`.
  - Los perfiles 21, 25 y 26 además fuerzan UTF-8 (`chcp 65001` y `JAVA_TOOL_OPTIONS`).
- **Perfil de automatización:** `cmd`.
- **Sesiones persistentes:** desactivadas.
- **Pestañas de terminal:** siempre visibles (`tabs.hideCondition: never`).
- **Esquemas de enlace permitidos:** `file`, `http`, `https`, `mailto`, `vscode`, `vscode-insiders`, `ms-settings`.

> **Atención:** `terminal.integrated.env.windows` fija `JAVA_HOME` en JDK 25, mientras que el perfil por defecto es JavaSE-26. Según el perfil, puede haber un desajuste de versión de Java en el terminal. Conviene unificarlo.

## 5. Configuración del workspace

### `.vscode/settings.json`

```json
{
    "java.configuration.updateBuildConfiguration": "interactive",
    "java.compile.nullAnalysis.mode": "automatic",
    "java.debug.settings.onBuildFailureProceed": true
}
```

### `.vscode/launch.json`: configuraciones de ejecución

| Nombre | Clase principal | Proyecto | `.env` |
|---|---|---|---|
| ApiGatewayApplication | `com.ecommerce.api_gateway.ApiGatewayApplication` | api-gateway | — |
| DiscoveryServerApplication | `com.ecommerce.discovery_server.DiscoveryServerApplication` | discovery-server | — |
| ProductServiceApplication | `com.ecommerce.product_service.ProductServiceApplication` | product-service | — |
| OrderServiceApplication | `com.ecommerce.order_service.OrderServiceApplication` | order-service | — |
| Spring Boot-InventoryServiceApplication | `com.ecommerce.inventory_service.InventoryServiceApplication` | inventory-service | `${workspaceFolder}/.env` |
| Spring Boot-ConfigServerApplication | `com.ecommerce.config_server.ConfigServerApplication` | config-server | `${workspaceFolder}/config-server/.env` |

## 6. Claude Code y Snyk

- `claudeCode.preferredLocation`: `panel`.
- Snyk: CLI en `...\AppData\Local\snyk-ls\snyk-win.exe`; carpeta de confianza: este workspace; configuración automática del servidor MCP de Snyk activada; notificación de bienvenida desactivada.

## 7. Extensiones instaladas (43)

### Java y Spring
`redhat.java`, `pleiades.java-extension-pack-jdk`, `vscjava.vscode-java-pack`, `vscjava.vscode-java-debug`, `vscjava.vscode-java-test`, `vscjava.vscode-java-dependency`, `vscjava.vscode-maven`, `vscjava.vscode-gradle`, `vscjava.vscode-lombok`, `vscjava.migrate-java-to-azure`, `vmware.vscode-boot-dev-pack`, `vmware.vscode-spring-boot`, `vscjava.vscode-spring-boot-dashboard`, `vscjava.vscode-spring-initializr`, `redhat.vscode-xml`

### Angular y frontend
`angular.ng-template`, `cyrilletuzi.angular-schematics`, `johnpapa.angular2`, `bradlc.vscode-tailwindcss`, `esbenp.prettier-vscode`, `formulahendry.auto-rename-tag`, `steoates.autoimport`, `ritwickdey.liveserver`, `ms-edgedevtools.vscode-edge-devtools`

### Calidad y seguridad
`sonarsource.sonarlint-vscode`, `snyk-security.snyk-vulnerability-scanner`, `usernamehw.errorlens`

### Git y contenedores
`eamodio.gitlens`, `ms-azuretools.vscode-containers`, `ms-vscode-remote.remote-containers`

### Productividad y estilo
`aaron-bond.better-comments`, `intellsmi.comment-translate`, `streetsidesoftware.code-spell-checker`, `editorconfig.editorconfig`, `johnpapa.vscode-peacock`, `mechatroner.rainbow-csv`, `oderwat.indent-rainbow`, `shardulm94.trailing-spaces`, `quicktype.quicktype`

### Tema, iconos e idioma
`enkia.tokyo-night`, `pkief.material-icon-theme`, `ms-ceintl.vscode-language-pack-es`

### IA
`anthropic.claude-code`

### Reinstalar todas las extensiones

```powershell
code --list-extensions > extensions.txt            # exportar
Get-Content extensions.txt | ForEach-Object { code --install-extension $_ }   # importar
```

## 8. Otros

- No hay `keybindings.json` ni snippets personalizados.
