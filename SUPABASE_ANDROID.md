# Conexión de Android con Supabase

Esta guía muestra cómo conectar tu aplicación Android directamente al backend de Supabase usando la librería [supabase-kt](https://github.com/supabase-community/supabase-kt).

---

## 1. Obtener credenciales
1. Ingresa a [tu dashboard de Supabase](https://supabase.com/dashboard/project/qllogpixdhmikwljbsgy/sql/new)
2. Ve a **Settings > API**
3. Copia:
   - `Project URL`: `https://qllogpixdhmikwljbsgy.supabase.co`
   - `Anon public API Key`: `<reemplaza_aquí>`

## 2. Agrega la dependencia
Abre tu archivo `build.gradle (Module)` y agrega:

```gradle
dependencies {
    implementation("io.github.jan-tennert.supabase:postgrest-kt:2.4.0")
}
```

Verifica la [última versión](https://github.com/supabase-community/supabase-kt#readme) si lo deseas.

---

## 3. Inicializa el cliente Supabase en tu código Kotlin

```kotlin
import io.github.jan.supabase.SupabaseClient
import io.github.jan.supabase.postgrest.Postgrest
import kotlinx.coroutines.runBlocking

val supabaseUrl = "https://qllogpixdhmikwljbsgy.supabase.co"
val supabaseKey = "TU_ANON_KEY" // Reemplaza aquí

val client = SupabaseClient(supabaseUrl, supabaseKey) {
    install(Postgrest)
}

fun getDataEjemplo() = runBlocking {
    val response = client.postgrest["mi_tabla"].select()
    println(response.data)
}
```

---

## 4. Notas de seguridad
No publiques tu Anon Key en repositorios públicos a menos que estés seguro de los permisos. Utiliza reglas RLS en Supabase para proteger tus datos.

---

¿Dudas? Consulta la [documentación oficial de Supabase](https://supabase.com/docs/guides/with-kotlin).

