# Gestión de Impresoras - UC HYO

Panel local que consulta por SNMP v2c el tóner y el papel disponible en las impresoras de `printers.json`.

El repositorio no incluye datos de impresoras ni direcciones IP de las sedes. En una instalación nueva, `Instalar.cmd` crea un `printers.json` vacío; las impresoras se agregan desde **Administrar**. `printers.example.json` es solo una plantilla.

Desde **Administrar** se puede cambiar el título del panel para identificar cada sede. Al registrar una impresora basta con ingresar su IPv4: el nombre se consulta por SNMP y puede editarse antes de guardar.

## Ejecutar

```powershell
go run .
```

Abrir `http://localhost:8080`.

## Instalar en Windows 11

1. Copiar toda la carpeta a una ubicación permanente, por ejemplo `C:\GestionImpresoras`.
2. Hacer clic derecho en `Instalar.cmd` y seleccionar **Ejecutar como administrador**.
3. Abrir desde otro equipo `http://IP-DEL-SERVIDOR:8080`.

La tarea se ejecuta en segundo plano con la cuenta `SYSTEM`, comienza inmediatamente al instalar y vuelve a iniciarse automáticamente si el proceso falla. El puerto TCP 8080 queda habilitado en todos los perfiles de red de Windows. `Desinstalar.cmd` elimina la tarea y la regla de firewall, pero conserva la configuración.

El instalador crea `printers.json` vacío solamente en una instalación nueva. En una actualización conserva tanto las impresoras registradas como el título personalizado guardado en `settings.json`.

La comunidad predeterminada es `public`. Puede cambiarse sin editar archivos:

```powershell
$env:SNMP_COMMUNITY = "otra-comunidad"
go run .
```

## Diagnóstico SNMP de bandejas

El ejecutable puede mostrar directamente en CMD la identificación y la tabla SNMP de bandejas:

```cmd
PrinterDashboard.exe --snmp-bandejas 10.120.40.12
```
