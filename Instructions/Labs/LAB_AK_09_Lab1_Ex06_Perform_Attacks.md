---
lab:
  title: 'Ejercicio 6: realización de ataques'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 6: realización de ataques

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex6.png)

Vas a simular los ataques que usarás más adelante para detectar e investigar en Microsoft Sentinel.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: ataque de persistencia con adición de clave del registro

>**Importante:** los pasos siguientes se realizan en una máquina diferente de aquella en la que estabas trabajando anteriormente. Busca el nombre de máquina virtual en la pestaña de referencias.

En esta tarea, realizarás ataques en el host conectado a Azure Arc que tiene configurado el agente de Azure Monitor.

1. Inicia sesión en la máquina virtual WINServer como administrador con la contraseña: **Pa55w.rd**.  

    >**Importante:** con la funcionalidad *SAVE* del laboratorio, WINServer se puede desconectar de Azure Arc. Si reinicias, se resolverá el problema.  

1. Selecciona **Iniciar** en Windows. Luego **Encendido**, luego **Reiniciar**.

1. Sigue las instrucciones para volver a iniciar sesión en WINServer.

1. En la búsqueda de la barra de tareas, escribe *Comando*. El símbolo del sistema se mostrará en los resultados de la búsqueda. Haz clic con el botón derecho en el símbolo del sistema y selecciona **Ejecutar como administrador**. Selecciona **Sí** en la ventana Control de cuentas de usuario que aparece para permitir que se ejecute la aplicación.

1. En el símbolo del sistema, crea una carpeta Temp en el directorio raíz. No olvides presionar Entrar después de la última fila:

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

1. Copia y ejecuta este comando para simular la persistencia del programa:

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```


### Tarea 2: ataque de elevación de privilegios con agregación de usuario

1. Copia y ejecuta este comando para simular la creación de una cuenta de administrador. No olvides presionar Entrar después de la última fila:

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

### Tarea 3: ataque de comando y control con DNS

1. Copia y ejecuta este comando para crear un script que simulará una consulta DNS en un servidor C2:

    ```CommandPrompt
    notepad c2.ps1
    ```

1. Selecciona **Sí** para crear un nuevo archivo y copia el siguiente script de PowerShell en *c2.ps1*.

    >**Nota:** Es posible que, al pegar en el archivo de máquina, se muestre la longitud completa del script. Asegúrate de que el script coincida con las instrucciones del archivo *c2.ps1*.

    ```PowerShell
    param(
        [string]$Domain = "microsoft.com",
        [string]$Subdomain = "subdomain",
        [string]$Sub2domain = "sub2domain",
        [string]$Sub3domain = "sub3domain",
        [string]$QueryType = "TXT",
        [int]$C2Interval = 8,
        [int]$C2Jitter = 20,
        [int]$RunTime = 240
    )
    $RunStart = Get-Date
    $RunEnd = $RunStart.addminutes($RunTime)
    $x2 = 1
    $x3 = 1 
    Do {
        $TimeNow = Get-Date
        Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        if ($x2 -eq 3 )
        {
            Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            $x2 = 1
        }
        else
        {
            $x2 = $x2 + 1
        }    
        if ($x3 -eq 7 )
        {
            Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            $x3 = 1
        }
        else
        {
            $x3 = $x3 + 1
        }
        $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
        Start-Sleep -Seconds $Jitter
    }
    Until ($TimeNow -ge $RunEnd)
    ```

1. En el menú Bloc de notas, selecciona **Archivo** y luego **Guardar**. 

1. En la ventana del símbolo del sistema, copia el siguiente comando y presiona Entrar. 

    >**Nota:** verás errores de resolución de DNS. Se espera que esto sea así.

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

>**Importante:** no cierres estas ventanas. Deja que este script de PowerShell se ejecute en segundo plano. El comando debe generar entradas de registro durante algunas horas. Puedes continuar con la siguiente tarea y los ejercicios siguientes mientras se ejecuta este script. Los datos creados por esta tarea se usarán en el laboratorio de búsqueda de amenazas más adelante. Este proceso no creará cantidades considerables de datos o procesamiento.

## Continúa con el ejercicio 7
