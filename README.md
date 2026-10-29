# Práctica 17 – Rutas protegidas e inscripciones

## Ejecutar

**Backend:**
```bash
cd backend
npx prisma generate
npx prisma db seed
npm run start:dev
```

**Frontend:**
```bash
npm install
npm run dev
```

---

## Ejercicio 1 – Mis inscripciones, sólo con sesión

### ¿La ruta protegida hace segura la aplicación? ¿Qué es lo que de verdad protege los datos?

No. La ruta protegida solo esconde la pantalla. Lo que de verdad protege los datos es el backend, que valida el token JWT en cada petición y devuelve 401 si no es válido.

### Comprobación con curl

```bash
curl http://localhost:3000/inscripciones/mias
# → 401 Unauthorized
```

---

## Ejercicio 2 – Inscribirse y el 401

### ¿Por qué no se manda el miembroId al inscribirse?

Porque el backend lo saca del token JWT. Mandarlo desde el cliente sería un riesgo, cualquiera podría cambiarlo para inscribirse como otra persona.

### ¿Qué diferencia hay entre un 401 y un 403?

- **401** – no sé quién eres (sin token o token inválido).
- **403** – sé quién eres, pero no tienes permiso (cuenta sin rol de miembro).

---

## Evidencias

Capturas en la carpeta `evidencias/`.
