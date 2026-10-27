# Práctica 16 – Sesión con JWT

En esta práctica se le agregó inicio de sesión al proyecto del gimnasio. Se usó React Context para manejar la sesión, JWT para autenticar contra el backend y un interceptor de Axios para mandar el token en cada petición.

## Ejercicio 1 – Contexto de sesión

### ¿Por qué se usa un contexto y no props para la sesión?

La sesión la necesitan componentes que están en partes muy distintas del árbol, como el encabezado, las páginas y los servicios. Si se pasara por props habría que ir de componente en componente aunque varios de ellos no la usen para nada. Con el contexto cualquiera la puede leer directamente sin ese lío de "prop drilling".

### ¿Qué pasa si un componente usa la sesión fuera del proveedor?

El hook `useSesion` lanza un error de forma intencional. Lo hicimos así para que el problema se detecte de inmediato en lugar de que falle de manera silenciosa o devuelva datos vacíos sin avisar.

## Ejercicio 2 – Login e interceptor

Se creó la página de inicio de sesión como formulario controlado y una página de registro. Cuando las credenciales son incorrectas se muestra el mensaje que devuelve la API directamente en el formulario.

Se agregó un interceptor de petición en Axios que adjunta el token guardado en cada solicitud:

```
Authorization: Bearer <token>
```

### ¿Dónde se guarda el token y qué riesgo tiene ese lugar?

El token se guarda en `localStorage`. La ventaja es que la sesión se mantiene aunque se recargue la página o se cierre la pestaña. El riesgo es que cualquier script que corra en la página puede leerlo, entonces si hubiera un ataque XSS el token quedaría expuesto. La alternativa más segura sería usar una cookie con la bandera `HttpOnly`, pero eso requiere más configuración en el backend.

## Evidencias

Las capturas están en la carpeta `evidencias/`:

- `06-credenciales-invalidas.png` – error al meter datos incorrectos
- `07-sesion-iniciada.png` – encabezado con el nombre del usuario y botón Salir
- `08-authorization.png` – header Authorization visible en la pestaña Red
- `09-jwt-io.png` – token decodificado en jwt.io
- `10-registro-nuevo.png` – cuenta nueva creada con el formulario de registro

## Ejecutar el proyecto

**Backend:**

```bash
cd backend
npx prisma generate
npx prisma db seed
npm run start:dev
```

> Las cuentas de prueba usan la contraseña `gimnasio2026`.

**Frontend:**

```bash
npm install
npm run dev
```
