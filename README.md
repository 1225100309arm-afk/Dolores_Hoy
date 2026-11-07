# 🏛️ Dolores Hoy 



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
