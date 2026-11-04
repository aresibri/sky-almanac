# Sky Almanac: guía del proyecto

Kiroween 2026 · Categoría **Frankenstein** · Entrega: **viernes 4 de diciembre de 2026, 2:00 PM hora del Pacífico** (entreguen el 2 o 3 de diciembre).

> Lo más antiguo del campo, con la ciencia de hoy: un almanaque de papel alimentado por 80 años de datos climáticos, con una asistente que te habla en tu idioma, y que funciona en la parcela aunque no haya señal.

---

## 1. Qué Kiro usar

| Herramienta | ¿La usamos? | Para qué |
|---|---|---|
| **Kiro IDE** (el programa que se descarga) | ✅ **La principal, las dos** | Aquí se construye todo: specs, steering, hooks, correr y probar la app |
| **Kiro Web** | Opcional, al final | Hacer 1 o 2 tareas pequeñas para poder contar en la entrega en qué se diferencia |
| **Kiro CLI** (en la terminal) | Opcional, al final | Igual que Kiro Web: probarlo una vez y anotar la diferencia |
| **Kiro Crew** | ❌ No | Es más cosas que aprender en un primer hackathon |

**¿Por qué combinar?** El texto de entrega pregunta: *"¿Usaron Kiro IDE, CLI, Web o Crew? ¿En qué se diferenciaron?"*. Construyan todo con el IDE y, en la semana 4, hagan una tarea pequeña con Kiro Web o CLI (por ejemplo, revisar las traducciones o escribir el README). Anoten la diferencia en `NOTAS-KIRO.md`. Eso suma puntos sin arriesgar el proyecto.

*Nota honesta: no conozco a detalle cómo funcionan Kiro Web, CLI y Crew. Revisen la documentación en kiro.dev antes de probarlos.*

---

## 2. Instalación (las dos, cada una en su compu)

### 2.1 Programas
1. **Kiro IDE:** https://kiro.dev → *Download* → Windows. Instalar y abrir. Inicien sesión con la **misma cuenta** con la que pedirán los créditos.
2. **Node.js:** https://nodejs.org → versión **LTS**. Instalar con las opciones por defecto.
3. **Git:** https://git-scm.com → Windows. Instalar con las opciones por defecto.

### 2.2 Comprobar
En Kiro: menú **Terminal → New Terminal** y escribir, uno por uno:
```
node --version
git --version
```
Cada uno debe responder con un número. Si no, cierren Kiro, vuelvan a abrirlo y prueben otra vez. Si sigue fallando, mándenme captura.

Luego configuren su nombre en Git (cada una con el suyo):
```
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
```

### 2.3 Cuentas y trámites
- [ ] Cuenta de **GitHub** (las dos).
- [ ] Pedir los **4,000 créditos gratis** en la pestaña *Resources* de la página del hackathon **antes del 1 de diciembre a las 12:00 PM PT**.
- [ ] Unirse al **Discord de Kiro**, canal `#kiroween-hackathon`.
- [ ] **LinkedIn** (las dos): lo piden para el premio de estudiantes.
- [ ] Registrarse en el hackathon en Devpost y crear el equipo (las dos).
- [ ] Opcional: la sesión de Devpost del **11 de noviembre, 10:00 AM PT**.

---

## 3. Crear el proyecto (lo hace una, la otra se une)

### Quien lo crea
1. En GitHub: **New repository** → nombre `sky-almanac` → **Public** → marcar *Add a README* → *Choose a license*: **MIT** → *Create*.
2. *Settings → Collaborators* → invitar a la otra.
3. En Kiro: *File → Clone Repository* (o en la terminal `git clone <url-del-repo>`), y abrir la carpeta.
4. Copiar dentro del repositorio la carpeta **`.kiro/`** de este paquete, junto con `SPECS.md` y `NOTAS-KIRO.md`.
5. Hacer el primer commit y push (ver la sección 5).

### Quien se une
1. Aceptar la invitación de GitHub (llega por correo).
2. En Kiro: clonar el mismo repositorio.

### ⚠️ Reglas que no se rompen
- **Nunca** poner `.kiro` en el `.gitignore`: es causa de descalificación.
- El repositorio debe ser **público** y tener la licencia visible.
- **Nunca** subir claves secretas (API keys) al repositorio.

---

## 4. Cómo se trabaja con Kiro

### Steering (ya está hecho)
Los archivos de `.kiro/steering/` son las "reglas de la casa". Kiro los lee siempre. Ya están escritos con todo lo que decidimos: qué es la app, la tecnología, offline-first, idiomas, honestidad, Doña Nube, diseño. Si algo cambia en el proyecto, se actualiza ahí.

### Specs (así se construye cada parte)
1. En el panel de Kiro, crear un **Spec** nuevo.
2. Pegar el texto del spec que toca, de `SPECS.md`.
3. Kiro escribe 3 documentos: **requisitos, diseño y tareas**. **Léanlos antes de aprobar.** Si algo no lo entienden, me lo pegan y lo revisamos.
4. Kiro ejecuta las tareas una por una. Revisen cada resultado y prueben la app (`npm run dev`).
5. Cuando el spec está terminado: commit y push.

Pueden hablarle a Kiro en español. Los specs quedan en inglés para que los jueces los lean.

### Hooks (automatizaciones)
En el spec 1 se crean dos hooks:
- **Pruebas automáticas:** cada vez que guardan un archivo de `src/engine/`, se corren las pruebas.
- **Revisor de traducciones:** cada vez que se agrega texto a la app, Kiro revisa que exista en los 7 idiomas.

### Referencias de diseño
Tomen capturas de pantalla de los prototipos que hicimos y guárdenlas en `docs/design/`. Cuando pidan un spec de pantallas, díganle a Kiro: *"usa las imágenes de docs/design como referencia"*.

---

## 5. Trabajar las dos en el mismo proyecto

Kiro está basado en VS Code y tiene un panel de **control de versiones** (el ícono de ramitas a la izquierda). La rutina:

1. **Antes de empezar a trabajar:** *Pull* (traer los cambios de la otra).
2. **Al terminar algo que funciona:** escribir un mensaje corto → *Commit* → *Push*.
3. **Nunca trabajen las dos en el mismo spec o en los mismos archivos al mismo tiempo.** Por eso cada una tiene sus carpetas (ver abajo).

Si Git muestra un "conflicto", no se asusten: mándenme el mensaje y lo resolvemos.

### Quién hace qué
| Tú (electrónica) | Ella (computación) |
|---|---|
| **El motor de cálculo** (`src/engine/`): la lluvia diaria es una señal en el tiempo. Detectar el inicio real de las lluvias, los periodos secos, los grados-día, las probabilidades, los años con El Niño y el **simulador** | **La app** (`src/app/`, `src/screens/`): la base del proyecto, la instalación sin internet, los idiomas, la ubicación con GPS y mapa, las pantallas, la cuenta y la publicación |
| La lógica de las respuestas de Doña Nube | La mascota animada de Doña Nube |
| Validar los datos de cultivos con alguien de agronomía | Conseguir quién revise el kichwa |

El diseño, el video y el texto de entrega los hacen juntas.

---

## 6. Plan de 5 semanas

| Semana | Fechas | Specs | Meta al terminar la semana |
|---|---|---|---|
| 1 | 2 – 8 nov | Instalar todo · **Spec 1** | Ver en pantalla la lluvia de 80 años de Portoviejo, guardada en el navegador |
| 2 | 9 – 15 nov | **Spec 2** · **Spec 3** | El motor calcula el inicio de lluvias y las probabilidades (con pruebas); idioma y ubicación funcionando |
| 3 | 16 – 22 nov | **Spec 4** · **Spec 5** | La pantalla "Tu almanaque" y el **simulador** con datos reales. Mostrarlo a alguien de agronomía |
| 4 | 23 – 29 nov | **Spec 6** · **Spec 7** · **Spec 8** | Herramientas, Doña Nube, modo sin internet e impreso. Probar Kiro Web o CLI. Escribir el blog y la publicación en redes. Revisión del kichwa |
| 5 | 30 nov – 3 dic | **Spec 9** (si da tiempo) · pulir | Video, texto de entrega y **entregar el 2 o 3 de diciembre** |

**Si se atrasan:** el spec 9 (cuentas) y la mascota animada son lo primero que se recorta. La app sigue completa con "Probar sin cuenta" y Doña Nube en el chat.

---

## 7. Lista para la entrega

- [ ] Categoría: **Frankenstein**.
- [ ] Repositorio público en GitHub, con licencia MIT visible y la carpeta `.kiro/`.
- [ ] URL de la app funcionando (publicada en Vercel).
- [ ] Botón "Probar sin cuenta" funcionando, para los jueces.
- [ ] Video de **menos de 3 minutos**, público en YouTube, sin música con derechos de autor. Incluir la escena en **modo avión**.
- [ ] Descripción del proyecto.
- [ ] Texto sobre cómo usaron Kiro (sale de `NOTAS-KIRO.md`).
- [ ] Premio de estudiantes: LinkedIn, correo de la universidad, semestre, carrera y universidad de cada una.
- [ ] Blog publicado, diciendo que es para Kiroween 2026, con el enlace en la entrega.
- [ ] Publicación en redes que **empiece** con `#KiroweenHackathon26`, con el enlace en la entrega.

## 8. Cosas que no hay que olvidar
- **Honestidad:** la app nunca dice "lloverá" ni "siembra tal día". Siempre "en X de cada 10 años".
- **Kichwa, hindi, indonesio y suajili** los revisa alguien que hable el idioma, o se marcan como traducción automática.
- **Datos de cultivos** (calor y agua que necesitan): confirmarlos con alguien de agronomía.
- **Anotar en `NOTAS-KIRO.md` desde el día 1.**
