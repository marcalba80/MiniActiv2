MiniActiv2
============================

1.Intentar compactar el codi, és a dir, evitar, si és possible, repetir codi en les diverses
  parts de l’app i encapsular en mètodes tot allò que s’utilitzi en més d’una ocasió.

  El codi contenia errors alhora de mostrar el snackbar de settings, un cop es denegaven els permisos, seleccionant que no es tornes a mostrar el missatge.
  Es produïa un bucle infinit, que llançava el snackbar de settings constantment, fet que deixava l'aplicació inutilitzada. A més aquest snackbar
  es llançava sempre independentment del tipus de denegació del permís que es selecciones.

  Un cop fetes aquestes correccions podem observar com el comportament de l'aplicació resultant, es coherent, s'ajusta als requirements i
  bones pràctiques dels permissos d'Android.

2.Explicar què fa el darrer mètode de MainActivity: onRequestPermissionsResult(...)

  Aquest mètode recull les accions que s'hauran de dur a terme, un cop s'ha cridat a demanar els permissos necessaris pel bon funcionament de l'aplicació,
  es llança automàticament un cop l'usuari a seleccionat alguna de les opcions disponibles sobre el permís demanat. En el nostre cas, gestionem quan l'usuari
  concedeix el permís i quan el denega permamentment.