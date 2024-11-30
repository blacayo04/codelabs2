

## 1. Android Kotlin Fundamentals: Create dynamic lists with RecyclerView vale 4 puntos https://developer.android.com/develop/ui/views/layout/recyclerview
implementation 'androidx.recyclerview:recyclerview:1.3.0'

<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recyclerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp" />

<TextView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/tvName"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="16dp"
    android:textSize="18sp"
    android:textColor="#000" />

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class NameAdapter(private val names: List<String>) : RecyclerView.Adapter<NameAdapter.NameViewHolder>() {

    class NameViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val tvName: TextView = view.findViewById(R.id.tvName)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): NameViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_name, parent, false)
        return NameViewHolder(view)
    }

    override fun onBindViewHolder(holder: NameViewHolder, position: Int) {
        holder.tvName.text = names[position]
    }

    override fun getItemCount(): Int = names.size
}

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val recyclerView: RecyclerView = findViewById(R.id.recyclerView)

        // Datos de ejemplo
        val names = listOf("Alice", "Bob", "Charlie", "Diana", "Edward")

        // Configuración del RecyclerView
        recyclerView.layoutManager = LinearLayoutManager(this)
        recyclerView.adapter = NameAdapter(names)
    }
}



## 2- Informe de investigación About fragments, Create a fragment, Fragment manager, Fragment transactions, Animate transitions between fragments, Fragment lifecycle, Saving state with fragments y Communicate with fragments: Entregarlo como un informe en word o slides vale 4 puntos 

**https://developer.android.com/guide/fragments?hl=es-419**

1.  Los fragments en Android son componentes reutilizables que representan partes de la interfaz de usuario dentro de una actividad. Funcionan como bloques modulares que permiten diseñar pantallas más flexibles, adaptables a diferentes dispositivos y orientaciones.

- Estructura básica:

- Un fragmento siempre está asociado a una actividad que actúa como su contenedor.
Puede tener su propio ciclo de vida, que está vinculado al ciclo de vida de la actividad principal.

- Uso y configuración:

- Se pueden agregar a una actividad mediante código (dinámicamente) o en el archivo de diseño XML (estáticamente).
Se utiliza la clase FragmentManager para manejar operaciones como agregar, reemplazar o eliminar fragments.



**https://developer.android.com/guide/fragments/create?hl=es-419**

2. El proceso de crear fragmentos en Android sigue pasos clave que ayudan a integrarlos correctamente dentro de una aplicación.

- Definir el diseño del fragmento:

- Se crea un archivo de diseño XML para el fragmento que contiene la interfaz de usuario deseada.
Crear una clase de fragmento:

- Se extiende la clase Fragment o una de sus variantes (como DialogFragment o ListFragment).
En el método onCreateView, se infla el diseño definido anteriormente.
Incluir el fragmento en la actividad:

- Puedes agregar el fragmento al diseño de una actividad utilizando el contenedor <fragment> en el archivo XML de la actividad o dinámicamente mediante el FragmentManager.
Administrar el ciclo de vida del fragmento:

- Los fragmentos tienen un ciclo de vida propio que se sincroniza con la actividad contenedora. Es crucial manejar métodos como onCreate, onStart, y onDestroy según sea necesario.
Interacciones entre actividad y fragmento:

- Las actividades pueden comunicarse con los fragmentos utilizando interfaces o métodos públicos para intercambiar datos o eventos.


**https://developer.android.com/guide/fragments/fragmentmanager?hl=es-419**

3. El FragmentManager es una clase fundamental en Android para gestionar el ciclo de vida de los fragments y realizar operaciones como agregar, eliminar, mostrar, ocultar y reemplazar fragments en una actividad o dentro de otros fragments.

- Gestión de Ciclo de Vida:
Controla las transiciones de estado de los fragments a través de su ciclo de vida, como CREATED, STARTED y RESUMED.
Usa métodos como onAttach() y onDetach() para realizar tareas cuando un fragment es asociado o desasociado de su actividad principal​
ANDROID DEVELOPERS
​
- Transacciones de Fragmentos:
Permite realizar cambios dinámicos en la interfaz de usuario usando FragmentTransaction, con métodos como add(), remove(), replace() y commit().
Las transacciones pueden agregarse a una pila de retroceso (back stack) para permitir navegación inversa, como regresar a un fragment anterior

- Comunicación entre Fragments:
Facilita la comunicación entre fragments mediante APIs como Fragment Result API. Por ejemplo, puedes usar setFragmentResultListener para pasar datos entre dos fragments sin referencias directas entre ellos.
Además, puedes compartir datos entre un fragment padre y sus hijos usando un ViewModel compartido​

- Uso de FragmentManager en XML y Código:
Se recomienda usar FragmentContainerView en lugar del <fragment> tag en XML para mayor control sobre el estado de los fragments​


- API de Resultados:
FragmentManager también integra la API de resultados para manejar flujos como startActivityForResult() y requestPermissions() sin necesidad de sobrecargar métodos dentro del fragment​

​
**https://developer.android.com/guide/fragments/transactions?hl=es-419**


4. En Android, las transacciones de fragmentos permiten agregar, reemplazar, o eliminar fragmentos dinámicamente durante el tiempo de ejecución. Estas operaciones se realizan mediante el FragmentManager, que organiza los fragmentos asociados a una actividad o a otros fragmentos. Las transacciones suelen manejarse a través de una instancia de FragmentTransaction, la cual permite personalizar el comportamiento visual de los fragmentos, como animaciones o efectos de transición.

- Operaciones comunes
Agregar (add): Incorpora un fragmento a un contenedor existente.
Reemplazar (replace): Sustituye un fragmento existente por otro.
Eliminar (remove): Quita un fragmento del contenedor.
Ocultar/mostrar (hide/show): Cambia la visibilidad de los fragmentos.
Uso del Back Stack
El back stack guarda un registro de las transacciones, permitiendo al usuario deshacerlas con el botón de retroceso. Esto se habilita mediante el método addToBackStack() durante la transacción.

- Animaciones
Puedes personalizar las transiciones entre fragmentos definiendo animaciones específicas mediante setCustomAnimations(), lo que mejora la experiencia de usuario con efectos visuales atractivos.

- Flujo básico
Obtén el FragmentManager de la actividad o fragmento.
Inicia una transacción con beginTransaction().
Realiza las operaciones deseadas (add, replace, etc.).
Opcionalmente, agrega la transacción al back stack.
Aplica los cambios con commit() o commitNow().

5. puedes mejorar la experiencia del usuario al agregar animaciones durante la navegación entre fragmentos. Existen dos enfoques principales para implementar estas animaciones:

- Framework de Animación:

- Utiliza las clases Animation y Animator para definir efectos como rotaciones, estiramientos, desvanecimientos y movimientos.

- Las animaciones se definen en archivos XML dentro del directorio res/anim.
- Se aplican mediante FragmentTransaction.setCustomAnimations(), especificando los recursos de animación para las transiciones de entrada y salida.

- Framework de Transiciones:

- Incluye transiciones de elementos compartidos entre fragmentos, como imágenes o vistas.
- Se definen en archivos XML en el directorio res/transition.
- Se aplican estableciendo las transiciones de entrada y salida en los fragmentos correspondientes.


## 3. Codelabs: Kotlin Basics vale 3 puntos
https://developer.android.com/training/basics/intents/sending?hl=es-419
import android.content.Intent
import android.content.pm.PackageManager
import android.net.Uri
import android.os.Bundle
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        
        val latitude = 48.8584
        val longitude = 2.2945

        
        val geoUri = Uri.parse("geo:$latitude,$longitude?q=$latitude,$longitude(Torre+Eiffel)")
        val mapIntent = Intent(Intent.ACTION_VIEW, geoUri)

        
        if (mapIntent.resolveActivity(packageManager) != null) {
            
            startActivity(mapIntent)
        } else {
            
            Toast.makeText(this, "No hay ninguna aplicación para ver mapas instalada", Toast.LENGTH_SHORT).show()
        }
    }
}


## 4. Codelabs: Functions vale 3 puntos

https://developer.android.com/codelabs/android-preferences-datastore?hl=es-419#8

- En imagenes. 


## 5. Informe de investigación acerca de Room: Entregarlo ya sea como Word o Slides o si se les ocurre algo mejor bienvenido sea vale 3 puntos

### Room es una librería de persistencia de datos de Android que proporciona una abstracción robusta y sencilla sobre SQLite. Es parte de Android Jetpack y está diseñada para garantizar prácticas seguras y eficientes al trabajar con bases de datos locales.

Ventajas de Room sobre SQLite
- Room mejora el manejo tradicional de bases de datos al proporcionar:

- Abstracción mediante anotaciones: Simplifica la creación y mantenimiento de bases de datos usando clases y anotaciones.
- Integración con LiveData y Flow: Facilita la observación de cambios en la base de datos, ideal para aplicaciones reactivas.
- Validación en tiempo de compilación: Detecta errores en consultas SQL antes de la ejecución.
- Mejor manejo de transacciones: Automatiza y optimiza operaciones como inserciones y actualizaciones.


Componentes Principales
- Room se basa en tres componentes fundamentales:

- Entidad (Entity):

- Representa una tabla en la base de datos.
- Es una clase anotada con @Entity.

@Entity(tableName = "users")
data class User(
    @PrimaryKey val id: Int,
    val name: String,
    val age: Int
)

- DAO (Data Access Object):

- Define métodos para interactuar con la base de datos (consultas, inserciones, actualizaciones).
- Se anota con @Dao.

@Dao
interface UserDao {
    @Query("SELECT * FROM users WHERE id = :id")
    fun getUserById(id: Int): LiveData<User>

    @Insert
    suspend fun insertUser(user: User)
}

- Base de datos:

- Es la clase que representa la base de datos, anotada con @Database.
- Proporciona instancias de los DAOs.
@Database(entities = [User::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}



## 6- Informe de investigación del patrón de arquitectura (Model View View-Model) MVVM: Entregarlo ya sea como Word o Slides o si se les ocurre algo mejor bienvenido sea vale 3 puntos

El patrón de arquitectura MVVM (Model-View-ViewModel) organiza el código de una aplicación separando la lógica de negocio, la presentación y la interfaz de usuario. Se diseñó para facilitar el mantenimiento, escalabilidad y pruebas del código, y es ampliamente utilizado en aplicaciones modernas, especialmente con frameworks como Android Jetpack.

1.  Modelo (Model):

- Representa la capa de datos y lógica de negocio.
- Puede interactuar con bases de datos, APIs u otros repositorios.
- No tiene conocimiento de la interfaz de usuario.

data class User(val id: Int, val name: String, val email: String)

2. Vista (View):

- Es la interfaz de usuario visible para el usuario.
- Recibe actualizaciones del ViewModel y representa los datos en la pantalla.
- En Android, las Activities o Fragments suelen actuar como vistas.
- Se mantiene lo más "tonta" posible, delegando toda la lógica al ViewModel.

3. ViewModel:

- Actúa como un puente entre la Vista y el Modelo.
- Gestiona la lógica de presentación y el estado de la interfaz de usuario.
- Puede contener datos observables como LiveData o StateFlow, lo que permite que la Vista se actualice automáticamente al cambiar los datos.

class UserViewModel : ViewModel() {
    private val _user = MutableLiveData<User>()
    val user: LiveData<User> get() = _user

    fun fetchUser(id: Int) {
        // Simulación de carga de datos
        _user.value = User(id, "John Doe", "johndoe@example.com")
    }
}

## 7- Infografía entre Volley y Retrofit: Entregarlo como una infografia o si se les ocurre algo mejor bienvenido sea vale 3 puntos
- En imagenes.


   
