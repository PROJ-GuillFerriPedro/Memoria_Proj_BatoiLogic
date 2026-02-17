# Pagina de login

En la pantalla de login tenemos varias cosas, de momento se tiene el usuario y contraseña en una variable (lo cual es muy malo para la seguridad).

Tenemos los imput que seran donde ponemos la información de login, el email que sera un imput de texto normal:

Imagen

Y el de contraseña, que escondera lo que escribas con este simbolo \*:



Luego los 2 campos comprovaran varias cosas, el de email comprovara que haya un @ y que no este vacio.

El de contraseña comprovara que haya 1 caracter en mayuscula,que haya 1 numero, que sea mayor de 8 caracteres y que tenga al menos 1 simbolo especial($·"%).

En los ultimos cambios de esta pantalla se le han añadido varias cosas:

* La primera seria que cuando se inicie la sesion se recojan los pedidos asignados en la api para ponerla en una base de datos local.
* Segundo guarda el inicio de sesion en localpreferences.
* Y tercero que si detecta que ha pasado menos de un dia desde el inicio de sesion te inicia automaticamente.



Luego de eso al darle al boton de login

{% @github-files/github-code-block url="https://github.com/PROJ-GuillFerriPedro/Aplicacion-Android-Repartidors/blob/main/lib/screens/LoginScreen.dart" visible="true" fullWidth="false" %}
