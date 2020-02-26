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

  El metode callback onRequestPermissionsResult() serveix per gestionar les respostes a la solicitud de permisos, en aquest cas de localització, que s’ofereix a l’usuari.
```java
  // Revisa que sigui la resposta a una petició de permisos
  if (requestCode == REQUEST_PERMISSIONS_REQUEST_CODE) {
     // Comprova que s’ha interactuat amb el cuadre de dialeg.
     if (grantResults.length <= 0) {
      // Es verifica que s’ha garantit el permis necesari
      } else if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
         if (mRequestingLocationUpdates) {
             startLocationUpdates();
          }
      // Si s’han denegat els permisos
      } else {
          // Es mostra que són imprecindibles, es dirigeix a settings
         boolean showRequestRationale = ActivityCompat.shouldShowRequestPermissionRationale(this,
                        Manifest.permission.ACCESS_FINE_LOCATION);
            if (!showRequestRationale){
                showSnackbar(R.string.permission_denied_explanation,
                        R.string.settings, new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {
                        // Build intent that displays the App settings screen.
                        Intent intent = new Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS);
                        Uri uri = Uri.fromParts("package", getPackageName(), null);
                        intent.setData(uri);
                        startActivityForResult(intent, REQUEST_CHECK_SETTINGS);
                    }
                });

                isRequestRequired = false;
            }
      }
   }    
```
