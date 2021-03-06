---
title: Enlazar eclipse con redmine
date: 2014-10-01T04:15:23+00:00
categories:
  - Coding
tags:
  - configuration
  - eclipse
  - redmine

---
<p style="text-align: justify">
  Suelo usar <strong>redmine</strong> como gestor de tareas y <strong>eclipse</strong> como mi IDE principal para programar, tanto en Java como en PHP.
</p>

<img class="decoded alignnone" src="https://2.bp.blogspot.com/-0eCQaME0TRg/ULerJTClnEI/AAAAAAAABag/tpAn1Onro8Q/s1600/ec_kepler.png" alt="Eclipse logo" width="211" height="211" /><img class="decoded alignnone" src="https://www.drupal.org/files/project-images/Redmine_logo_0.png" alt="redmine logo" width="212" height="212" />


<p style="text-align: justify">
  Hasta ahora utilizaba estas dos herramientas por separado, junto con un control de versiones, pero ya trabajo con ambas herramientas enlazadas de forma que en eclipse puedo marcar en qué tarea estoy trabajando. ¿Qué ventajas tiene esto? Simplemente tratar de no volverme loco entre tantos archivos. Y es que, aunque me gustaría, no puedo trabajar en una tarea hasta terminarla, cerrarla y empezar con otra. Casi siempre tengo que llevar 3 ó 4 tareas a la vez y con cada una de ellas tengo que estar abriendo unos cuantos archivos. Al final acabo no sabiendo qué archivos son de cada tarea o bien cerrándolos porque me pierdo entre ellos. Una solución ante esto es lo que hace un compañero de trabajo: tener varios grupos de ventanas en eclipse (uno por tarea) y en cada grupo están abiertos todos los archivos de dicha tarea.
</p>

<p style="text-align: justify">
  Pero la verdad es que como no me convencía esa solución me puse a investigar y descubrí que con Mylyn puedo enlazar en eclipse las tareas de redmine y cada tarea guarda su pequeño entorno de trabajo de forma que cada tarea sabe qué archivos tiene abiertos. Puedo, por tanto, cambiar de tarea y se me abren los archivos de dicha tarea cerrándose los de la tarea anterior.
</p>

## Instalemos lo que eclipse necesita

<p style="text-align: justify">
  Para empezar necesitamos tener redmine instalado, yo estoy usando la versión 2.4.2.stable. Además, por supuesto, debes tener instalado eclipse, actualmente tengo la versión Kepler. Eclipse usa el plugin Mylyn (que seguramente ya tengas instalado) para gestionar la lista de tareas. Este plugin lo puedes conectar a muchas fuentes de información: Jira, Trac, Mantis, etc. Cada gestor de tareas tiene un conector diferente que también debes instalar en eclipse. Si no existe el conector para tu programa de gestión de proyectos o bien no lo quieres usar existe otra opción, instalar un conector web que parsee la información que lees en la web del gestor de tareas. Ésta es la configuración que he utilizado para conectar eclipse &#8211; mylyn &#8211; redmine.
</p>

<p style="text-align: justify">
  Este conector web genérico no viene instalado por defecto en eclipse (como los otros), así que es necesario instalarlo, se trata del plugin <strong>Incubator</strong>. Él es quien se encarga de realizar la conexión a la web que se le indique. Yo instalé la versión 3.10 porque es la versión de Mylyn que tengo instalada en eclipse.
</p>

En resumen, éstos son los plugins a instalar en eclipse:

  * Mylyn: https://download.eclipse.org/mylyn/releases/latest
  * Incubator: https://download.eclipse.org/mylyn/incubator/3.10

## Instalar Incubator

<p style="text-align: justify">
  Ésta fue la parte que me costó más porque no conseguí encontrar este plugin en el marketplace de eclipse así que tuve que averiguar la URL del mismo, darla de alta en eclipse y obtener el plugin que está alojado en ella.
</p>

Para ello hay que ir al menú:

<pre class="lang:default highlight:0 decode:true ">Help -&gt; Install new software...</pre>

<p style="text-align: justify">
  En la ventana que se abre hacer clic en Add para añadir un nuevo repositorio de software.
</p>

{{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.24.49.png" title="Add incubator repository to eclipse" >}}

<p style="text-align: justify">
  Pon un nombre a este repositorio y la URL. Una vez creado eclipse se conecta al mismo y descarga el software disponible para que selecciones el que quieres instalar:
</p>

<p style="text-align: justify">
{{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.28.00.png" title="Instalando Mylyn Incubator" >}}

  Hacer clic en siguiente, aceptar la licencia y el software se empezará a instalar y seguramente cuando termine te pedirá reiniciar eclipse.
</p>

## Configurar eclipse para conectarse a redmine

<p style="text-align: justify">
  Una vez está todo instalado tendrás que abrir la vista &#8216;<em>Task list</em>&#8216;.
</p>

{{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.32.33.png" title="Eclipse - abrir task list" >}}

<p style="text-align: justify">
  En la vista que se ha abierto haz clic en el botón derecho y pulsa &#8216;new query'

{{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.37.01.png" title="Eclipse - task list - new query" >}}


  Esto abre una nueva ventana para seleccionar el repositorio de tareas, es decir, donde eclipse se va a conectar para leer las tareas que va a mostrar en la ventana task list. Por defecto aparece uno solo: Eclipse.org. Tendremos que añadir uno nuevo en el botón &#8216;Add Task Repository'. Si por contra quisiéramos añadir uno de los conectores preconfigurados usaríamos el botón &#8216;Install more connectors'. Ahora se abre una nueva ventana, en ella seleccionamos &#8216;<strong>Web Template (Advanced)</strong>&#8216;.
</p>

<p style="text-align: justify">
  {{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.40.38.png" title="Eclipse - conectara a redmine" >}}

  En la siguiente ventana hay que configurar este conector genérico para que sepa a qué URL conectarse, si debe usar usuario y contraseña para ello y cuál es la URL para obtener las tareas.
</p>

Para la conexión con redmine introducir los siguientes parámetros:

<pre class="lang:default decode:true">
Server:                 https://www.redmine.org -- Replace it with the URL of your Redmine instance
Task URL:               ${serverUrl}/issues/
New task URL:           ${serverUrl}/projects/appjose/issues/new -- Replace appjose with the identifier of the project used for new tasks
Query request URL:      ${serverUrl}/issues
Query pattern:          &lt;td class="tracker"&gt;({Type}.+?)&lt;/td&gt;&lt;td class="status"&gt;({Status}.+?)&lt;/td&gt;.+?&lt;td class="subject"&gt;.*?&lt;a href=".*?/issues/({Id}\d+)"&gt;({Description}.+?)&lt;/a&gt;&lt;/td&gt;({Optional}&lt;td class="assigned_to"&gt;&lt;a href.+?&gt;({Owner}.+?)&lt;/a&gt;&lt;/td&gt;)?
Login request URL:      ${serverUrl}/login?username=${userId}&password=${password}&authenticity_token=${loginToken} [POST]
Login Form URL:         ${serverUrl}/login
Login Token Pattern:    &lt;input name="authenticity_token" type="hidden" value="(.+?)" /&gt;</pre>

&nbsp;

<p class="lang:default decode:true">
  {{< figure src="/development/eclipse/Captura-de-pantalla-2014-10-01-a-las-05.49.06.png" title="Eclipse - conect to redmine repository" >}}
</p>

<p style="text-align: justify">
  El repositorio ahora se sincroniza y obtiene la información de las tareas que aparecerá en la task view.
</p>

&nbsp;

&nbsp;

Para más información sobre cómo configurar la conexión: <https://www.redmine.org/projects/redmine/wiki/HowTo_Mylyn>
