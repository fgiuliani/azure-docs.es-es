---
title: 'Personalización de las propiedades de RDP con PowerShell: Azure'
description: Cómo personalizar las propiedades de EDP para Windows Virtual Desktop con cmdlets de PowerShell.
services: virtual-desktop
author: Heidilohr
ms.service: virtual-desktop
ms.topic: how-to
ms.date: 03/30/2020
ms.author: helohr
manager: lizross
ms.openlocfilehash: eeab433bbbfc9db0f1c5f5546ae80434899a91dc
ms.sourcegitcommit: dabd9eb9925308d3c2404c3957e5c921408089da
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2020
ms.locfileid: "86259219"
---
# <a name="customize-remote-desktop-protocol-properties-for-a-host-pool"></a>Personalización de las propiedades de Protocolo de escritorio remoto para un grupo de hosts

>[!IMPORTANT]
>Este contenido se aplica a la versión de otoño de 2019 que no admite objetos de Windows Virtual Desktop para Azure Resource Manager. Si está tratando de administrar objetos de Windows Virtual Desktop para Azure Resource Manager incorporados en la actualización de primavera de 2020, consulte [este artículo](../customize-rdp-properties.md).

La personalización de las propiedades de Protocolo de escritorio remoto (RDP) de un grupo de hosts, como el uso de varios monitores y la redirección de audio, permite ofrecer una experiencia óptima a los usuarios en función de sus necesidades. Las propiedades de RDP se pueden personalizar en Windows Virtual Desktop mediante el parámetro **- CustomRdpProperty** del cmdlet **conjunto RdsHostPool**.

En [Configuración admitida del archivo RDP](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/rdp-files?context=/azure/virtual-desktop/context/context) encontrará una lista completa de las propiedades admitidas y sus valores predeterminados.

En primer lugar y, si aún no lo ha hecho, [descargue e importe el módulo de PowerShell para Windows Virtual Desktop](/powershell/windows-virtual-desktop/overview/) que se usará en la sesión de PowerShell. Después, ejecute el siguiente cmdlet para iniciar sesión en su cuenta:

```powershell
Add-RdsAccount -DeploymentUrl "https://rdbroker.wvd.microsoft.com"
```

## <a name="default-rdp-properties"></a>Propiedades predeterminadas de RDP

De forma predeterminada, los archivos RDP publicados contienen las siguientes propiedades:

|Propiedades de RDP | Escritorios | RemoteApps |
|---|---| --- |
| Modo multimonitor | habilitado | N/D |
| Redireccionamiento de unidad habilitado | Unidades, portapapeles, impresoras, puertos COM, dispositivos USB y tarjetas inteligentes| Unidades, Portapapeles e impresoras |
| Modo de audio remoto | Reproducción local | Reproducción local |

Las propiedades personalizadas que defina para el grupo host invalidarán estos valores predeterminados.

## <a name="add-or-edit-a-single-custom-rdp-property"></a>Adición y edición de una sola propiedad de RDP personalizada

Para agregar o editar una sola propiedad de RDP personalizada, ejecute el siguiente cmdlet de PowerShell:

```powershell
Set-RdsHostPool -TenantName <tenantname> -Name <hostpoolname> -CustomRdpProperty "<property>"
```

> [!div class="mx-imgBorder"]
> ![Captura de pantalla del cmdlet de PowerShell Get-RDSRemoteApp con el nombre y el nombre descriptivo resaltado](../media/singlecustomrdpproperty.png)

## <a name="add-or-edit-multiple-custom-rdp-properties"></a>Adición y edición de varias propiedades de RDP personalizadas

Para agregar o modificar varias propiedades de RDP personalizadas, ejecute los siguientes cmdlets de PowerShell, pero utilice las propiedades de RDP personalizadas como una cadena separada por punto y coma:

```powershell
$properties="<property1>;<property2>;<property3>"
Set-RdsHostPool -TenantName <tenantname> -Name <hostpoolname> -CustomRdpProperty $properties
```

> [!div class="mx-imgBorder"]
> ![Captura de pantalla del cmdlet de PowerShell Get-RDSRemoteApp con el nombre y el nombre descriptivo resaltado](../media/multiplecustomrdpproperty.png)

## <a name="reset-all-custom-rdp-properties"></a>Restablecimiento de todas las propiedades de RDP personalizadas

Las propiedades de RDP personalizadas se pueden restablecer a sus valores predeterminados. Para ello, solo hay que seguir las instrucciones de [Adición o edición de una sola propiedad de RDP personalizada](#add-or-edit-a-single-custom-rdp-property), o bien se pueden restablecer todas las propiedades de RDP personalizadas de un grupo de hosts ejecutando el siguiente cmdlet de PowerShell:

```powershell
Set-RdsHostPool -TenantName <tenantname> -Name <hostpoolname> -CustomRdpProperty ""
```

> [!div class="mx-imgBorder"]
> ![Captura de pantalla del cmdlet de PowerShell Get-RDSRemoteApp con el nombre y el nombre descriptivo resaltado](../media/resetcustomrdpproperty.png)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha personalizado las propiedades de RDP grupo de hosts especificado, puede iniciar sesión en un cliente de Windows Virtual Desktop para realizar pruebas como parte de una sesión de usuario. Estos dos procedimientos siguientes le indicarán cómo conectarse a una sesión mediante el cliente que elija:

- [Conexión con el cliente de Escritorio de Windows](connect-windows-7-10-2019.md)
- [Conexión con el cliente web](connect-web-2019.md)
