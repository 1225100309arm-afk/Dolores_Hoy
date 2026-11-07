#  Dolores Hoy 



##  Cómo ejecutarlo

```bash
flutter pub get
flutter test
flutter run --dart-define-from-file=secrets.json
```



##  Evidencias

### Código

** · `pubspec.yaml`: solo el paquete http**
![C1](capturas/C1_pubspec.png)

** · `.gitignore`: secretos fuera del repositorio**
![C2](capturas/C2_gitignore.png)

** · `secrets.json.example`: plantilla sin la clave real**
![C3](capturas/C3_secrets_example.png)

** · ClienteSeguro: las 6 defensas**
![C4](capturas/C4_cliente_seguro.png)

** · `redactar()`: logs sin claves**
![C5](capturas/C5_redactar.png)

** · API 1 · Clima**
![C6](capturas/C6_clima.png)

** · API 2 · Tipo de cambio (tasa inversa)**
![C7](capturas/C7_cambio.png)

** · API 3 · Festivos con fecha inyectada**
![C8](capturas/C8_festivos.png)

** · API 4 · Wikipedia: validación y `pathSegments`**
![C9](capturas/C9_wikipedia.png)

** · ConfigClaves: la clave entra al compilar**
![C10](capturas/C10_config_claves.png)

** · API 5 · Servicio NASA**
![C11](capturas/C11_nasa.png)

** · Validar la salida: `media_type` y solo https**
![C12](capturas/C12_foto_astronomica.png)

** · ViewModel: 5 APIs en paralelo**
![C13](capturas/C13_viewmodel.png)

** · TarjetaCarga: cargando / error / listo**
![C14](capturas/C14_tarjeta.png)

### Pruebas

** · Path injection: `../../admin` no se escapa de la ruta**
![P1](capturas/P1_path_injection.png)

** · `http://` se rechaza sin hacer la petición**
![P2](capturas/P2_solo_https.png)

** · La clave nunca se imprime completa**
![P3](capturas/P3_clave_oculta.png)

** · Si una API falla, las otras 4 siguen**
![P4](capturas/P4_resiliencia.png)

---
<img width="1277" height="952" alt="Captura de pantalla 2026-11-06 204251" src="https://github.com/user-attachments/assets/06e863cd-68b9-4591-a9c0-b4a50b0eda4d" />
