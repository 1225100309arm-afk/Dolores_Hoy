# 🏛️ Dolores Hoy — 5 APIs con seguridad

Tablero en Flutter hecho con **TDD** que muestra en una sola pantalla 5 datos de Dolores Hidalgo, cada uno de una API gratuita distinta, aplicando **buenas prácticas de seguridad**.

| # | API | Qué muestra | ¿Clave? |
|---|---|---|---|
| 1 | Open-Meteo | Clima actual de Dolores Hidalgo | No |
| 2 | Frankfurter | Tipo de cambio peso-dólar-euro | No |
| 3 | Nager.Date | Próximos días festivos de México | No |
| 4 | Wikipedia (es) | Resumen de "Dolores Hidalgo" | No (recibe texto del usuario) |
| 5 | NASA APOD | Foto astronómica del día | **Sí** |

- **Materia:** Desarrollo Móvil Integral · UTNG
- **Profesor:** Anastacio Rodríguez García
- **Alumna:** Yaneli Sánchez Cárdenas · Grupo GTID244

---

## 📋 ¿Qué se hizo? (resumen por ronda)

| Ronda | Qué se construyó | Archivo(s) |
|---|---|---|
| 0 | Proyecto con el paquete `http`, `.gitignore` para secretos y `secrets.json.example` | `pubspec.yaml`, `.gitignore` |
| 1 | Se leyó la documentación de las 5 APIs y se probaron las URLs en el navegador | — |
| 2 | `ClienteSeguro`: una sola "puerta" a internet con 6 defensas (solo https, timeout de 8 s, límite de 1 MB, JSON validado, errores traducidos, User-Agent) | `cliente_seguro.dart`, `excepciones.dart` |
| 3 | API 1 · Clima, con validación de coordenadas | `servicios.dart`, `modelos.dart` |
| 4 | API 2 · Tipo de cambio (tasa inversa: 1 / 0.05 = 20 pesos) | `servicios.dart`, `modelos.dart` |
| 5 | API 3 · Festivos, con la fecha de "hoy" inyectada para que las pruebas no caduquen | `servicios.dart` |
| 6 | API 4 · Wikipedia: validar, codificar con `pathSegments` (evita *path injection*) y aceptar solo imágenes https | `servicios.dart` |
| 7 | API 5 · NASA: la clave entra con `--dart-define`, nunca se imprime completa y se valida antes de pedir | `config_claves.dart` |
| 8 | ViewModel: las 5 APIs en paralelo; si una falla, las otras siguen funcionando | `tablero_viewmodel.dart` |
| 9 | Pantalla con `TarjetaCarga<T>` y "jalar para recargar" | `pantalla_tablero.dart`, `main.dart` |

### Ciclo TDD
🔴 **ROJO:** prueba primero (falla) → 🟢 **VERDE:** código mínimo → 🔵 **REFACTOR:** ordenar sin romper nada.
Todas las pruebas usan `MockClient`: **no necesitan internet** y no gastan el límite de las APIs.

### Corrección hecha al código del manual
En `ClienteSeguro.redactar()`, Dart convierte `***` en `%2A%2A%2A` dentro de la URL, y por eso la prueba `contains('api_key=***')` no pasaba. Se agregó `.replaceAll('%2A', '*')` para que el log muestre `api_key=***`.

### Estructura
```
lib/
  dominio/       <- excepciones y modelos
  datos/         <- ClienteSeguro, ConfigClaves y los 5 servicios
  presentacion/  <- ViewModel y pantalla
  main.dart
test/            <- 39 pruebas (cliente, seguridad, servicios, viewmodel)
```

---

## ▶️ Cómo ejecutarlo

```bash
flutter pub get
flutter test
flutter run --dart-define-from-file=secrets.json
```

`secrets.json` **no se sube a GitHub** (está en `.gitignore`). Para crear el tuyo, copia `secrets.json.example` y pon tu clave de https://api.nasa.gov (o deja `DEMO_KEY`).

---

## 📸 Evidencias

### Código

**C1 · `pubspec.yaml`: solo el paquete http**
![C1](capturas/C1_pubspec.png)

**C2 · `.gitignore`: secretos fuera del repositorio**
![C2](capturas/C2_gitignore.png)

**C3 · `secrets.json.example`: plantilla sin la clave real**
![C3](capturas/C3_secrets_example.png)

**C4 · ClienteSeguro: las 6 defensas**
![C4](capturas/C4_cliente_seguro.png)

**C5 · `redactar()`: logs sin claves**
![C5](capturas/C5_redactar.png)

**C6 · API 1 · Clima**
![C6](capturas/C6_clima.png)

**C7 · API 2 · Tipo de cambio (tasa inversa)**
![C7](capturas/C7_cambio.png)

**C8 · API 3 · Festivos con fecha inyectada**
![C8](capturas/C8_festivos.png)

**C9 · API 4 · Wikipedia: validación y `pathSegments`**
![C9](capturas/C9_wikipedia.png)

**C10 · ConfigClaves: la clave entra al compilar**
![C10](capturas/C10_config_claves.png)

**C11 · API 5 · Servicio NASA**
![C11](capturas/C11_nasa.png)

**C12 · Validar la salida: `media_type` y solo https**
![C12](capturas/C12_foto_astronomica.png)

**C13 · ViewModel: 5 APIs en paralelo**
![C13](capturas/C13_viewmodel.png)

**C14 · TarjetaCarga: cargando / error / listo**
![C14](capturas/C14_tarjeta.png)

### Pruebas

**P1 · Path injection: `../../admin` no se escapa de la ruta**
![P1](capturas/P1_path_injection.png)

**P2 · `http://` se rechaza sin hacer la petición**
![P2](capturas/P2_solo_https.png)

**P3 · La clave nunca se imprime completa**
![P3](capturas/P3_clave_oculta.png)

**P4 · Si una API falla, las otras 4 siguen**
![P4](capturas/P4_resiliencia.png)

---

## ✅ Checklist de seguridad
- [x] Ninguna clave en el código ni en el repositorio (`secrets.json` ignorado).
- [x] Todas las peticiones usan https y el cliente rechaza http.
- [x] Toda petición tiene timeout y límite de tamaño.
- [x] Las URLs se construyen con `Uri.https` / `pathSegments`.
- [x] Se valida la entrada del usuario y la salida del servidor.
- [x] Los logs usan `redactar()` y `ConfigClaves` no imprime la clave completa.
- [x] Los errores inesperados muestran un mensaje genérico.
- [x] Una API caída no afecta a las demás.
