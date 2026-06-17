# 🚀 Guía de instalación — Espacio Contigo

Sigue estos pasos en orden. El proyecto estará en línea en menos de 1 hora, gratis.

---

## PASO 1 — Crear tu proyecto en Firebase

1. Ve a **https://console.firebase.google.com**
2. Inicia sesión con una cuenta Google
3. Clic en **"Agregar proyecto"**
4. Nombre del proyecto: `espaciocontigo` (o el que prefieras)
5. Desactiva Google Analytics (no es necesario) → **Crear proyecto**
6. Espera que termine y haz clic en **Continuar**

---

## PASO 2 — Activar Firestore (base de datos)

1. En el menú izquierdo de Firebase: **Compilar → Firestore Database**
2. Clic en **"Crear base de datos"**
3. Selecciona **"Comenzar en modo de producción"**
4. Elige la región más cercana: `us-east1` (para Venezuela es la mejor opción)
5. Clic en **Habilitar**

---

## PASO 3 — Aplicar las reglas de seguridad

1. Dentro de Firestore, ve a la pestaña **"Reglas"**
2. Borra todo lo que hay y pega el contenido del archivo `firestore.rules`
3. Clic en **"Publicar"**

> Estas reglas permiten que los usuarios escriban datos, pero solo el admin puede leerlos y modificarlos.

---

## PASO 4 — Activar Authentication (para el admin)

1. En el menú izquierdo: **Compilar → Authentication**
2. Clic en **"Comenzar"**
3. Ve a la pestaña **"Sign-in method"**
4. Activa **"Correo electrónico/contraseña"**
5. Ve a la pestaña **"Usuarios"** → **"Agregar usuario"**
6. Escribe tu correo y una contraseña segura → **Agregar**

> Este usuario será el único que puede entrar al panel de administrador.

---

## PASO 5 — Obtener tus credenciales de Firebase

1. Ve a **Configuración del proyecto** (ícono de engranaje ⚙️ junto a "Descripción general del proyecto")
2. Baja hasta la sección **"Tus apps"**
3. Clic en **"Agregar app"** → selecciona el ícono **Web (</>)**
4. Nombre de la app: `espaciocontigo-web` → **Registrar app**
5. Firebase te mostrará un bloque de código con `firebaseConfig`. Cópialo.

Verás algo como esto:
```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "espaciocontigo.firebaseapp.com",
  projectId: "espaciocontigo",
  storageBucket: "espaciocontigo.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

---

## PASO 6 — Pegar las credenciales en los archivos

Abre **`index.html`** y busca esta sección (cerca del final):
```js
const firebaseConfig = {
  apiKey:            "TU_API_KEY",
  authDomain:        "TU_PROYECTO.firebaseapp.com",
  ...
};
```
Reemplaza los valores con los tuyos.

Haz exactamente **lo mismo en `admin.html`** — tiene la misma sección de configuración.

---

## PASO 7 — Publicar el proyecto (gratis con Netlify)

Esta es la forma más fácil y no necesita instalar nada.

1. Ve a **https://netlify.com** y crea una cuenta gratis
2. En el dashboard, busca el recuadro que dice **"Deploy manually"**
3. **Arrastra la carpeta `espaciocontigo`** completa a ese recuadro
4. Netlify la sube automáticamente y te da una URL como:
   `https://espaciocontigo-abc123.netlify.app`

¡Listo! Tu app ya está en internet.

### Para actualizar el sitio después:
Simplemente arrastra la carpeta de nuevo a Netlify. Se actualiza en segundos.

### Para tener un dominio personalizado (ej. espaciocontigo.org):
- En Netlify ve a **Domain settings → Add custom domain**
- Dominios `.org` o `.com` cuestan ~$10-15/año en Namecheap o Google Domains

---

## PASO 8 — Entrar al panel de administrador

Una vez publicado, tu panel de admin está en:
```
https://TU-URL.netlify.app/admin.html
```

Entra con el correo y contraseña que creaste en el Paso 4.

---

## ESTRUCTURA DE ARCHIVOS

```
espaciocontigo/
├── index.html        ← App principal para usuarios
├── admin.html        ← Panel de administrador
├── firestore.rules   ← Reglas de seguridad (solo para Firebase Console)
└── GUIA.md           ← Este archivo
```

---

## COLECCIONES EN FIRESTORE (se crean automáticamente)

| Colección | Qué guarda |
|---|---|
| `evaluaciones` | Estado de ánimo y preocupaciones de cada sesión |
| `mensajes` | Conversaciones del chat (usuario, bot y admin) |
| `respuestas_admin` | Mensajes que tú envías a los usuarios |
| `alertas` | Señales de crisis detectadas automáticamente |
| `contactos` | Solicitudes de contacto vía WhatsApp |

---

## FLUJO DE CRISIS (cómo funciona)

1. Un usuario escribe palabras de riesgo ("no quiero vivir", etc.)
2. El sistema detecta la señal y guarda una alerta en Firestore con nivel `crisis`
3. Tú ves la alerta en tiempo real en **admin.html → Alertas**
4. Puedes responderle desde la pestaña **Mensajes**
5. El usuario ve tu respuesta en su chat, marcada como "Orientador"
6. Marcar la alerta como "Atendida" la saca de la lista de pendientes

---

## COSTOS

| Servicio | Costo |
|---|---|
| Firebase Firestore | Gratis hasta 50.000 lecturas/día y 20.000 escrituras/día |
| Firebase Auth | Gratis sin límite de usuarios |
| Netlify Hosting | Gratis para proyectos estáticos |
| Total mes 1 | **$0** |

Con el plan gratuito de Firebase puedes atender cómodamente hasta varios miles de usuarios al mes. Si creces más, el costo de Firebase es muy bajo (~$25/mes por uso intensivo).

---

## PRÓXIMOS PASOS RECOMENDADOS

- [ ] Conseguir aliados: Sociedad Venezolana de Psiquiatría, FEVEMO, universidades con clínicas psicológicas
- [ ] Agregar el número de WhatsApp Business propio para contactar usuarios
- [ ] Registrar un dominio (.org o .com.ve) para darle mayor credibilidad
- [ ] Crear una cuenta de Instagram/Twitter para difundir la herramienta
- [ ] Configurar alertas por correo cuando lleguen nuevas crisis (Firebase Extensions → Trigger Email)

---

## SOPORTE

Si algo no funciona, revisa:
- Que las credenciales en `index.html` y `admin.html` sean exactamente iguales
- Que las reglas de Firestore estén publicadas (Paso 3)
- Que el usuario admin exista en Firebase Authentication (Paso 4)

---

*Espacio Contigo — Construido con ❤️ para Venezuela*
