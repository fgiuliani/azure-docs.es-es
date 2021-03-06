---
title: Asignar un usuario o grupo a una aplicación empresarial en Azure AD
description: Procedimiento para seleccionar una aplicación empresarial para asignarla a un usuario o un grupo en la versión preliminar de Azure Active Directory
services: active-directory
author: kenwith
manager: celestedg
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: how-to
ms.date: 02/21/2020
ms.author: kenwith
ms.reviewer: luleon
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eeab9cbb68567b6af3b1381b8ec5e67e82461ec
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "84763744"
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a>Asignación de un usuario o un grupo a una aplicación empresarial en Azure Active Directory

En este artículo se explica cómo asignar usuarios o grupos a aplicaciones empresariales en Azure Active Directory (Azure AD), ya sea desde Azure Portal o usando PowerShell. Cuando un usuario se asigna a una aplicación, dicha aplicación aparece en el [panel de acceso Mis aplicaciones](https://myapps.microsoft.com/) del usuario para que pueda acceder a ella más fácilmente. Si la aplicación expone roles, también se puede asignar un rol concreto al usuario.

De cara a tener un mayor control, se pueden configurar algunos tipos de aplicaciones empresariales para [requerir la asignación de usuarios](#configure-an-application-to-require-user-assignment). 

Para [asignar un usuario o grupo a una aplicación empresarial](#assign-users-or-groups-to-an-app-via-the-azure-portal), deberá iniciar sesión como un administrador global, un administrador de aplicaciones o un administrador de aplicaciones en la nube, o bien como el propietario de la aplicación empresarial.

> [!NOTE]
> La asignación basada en grupos requiere Azure Active Directory Premium P1 o P2. La asignación basada en grupo se admite en grupos de seguridad únicamente. Actualmente no se admiten las pertenencias a grupos anidados y los grupos de Office 365. Para conocer más requisitos de licencia de las características abordadas en este artículo, vea la [página de precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory). 

## <a name="configure-an-application-to-require-user-assignment"></a>Configuración de una aplicación para que requiera la asignación de usuarios

En los siguientes tipos de aplicaciones existe la opción de requerir que los usuarios estén asignados a la aplicación para poder acceder a ella:

- Aplicaciones configuradas para el inicio de sesión único (SSO) federado con autenticación basada en SAML
- Aplicaciones de proxy de aplicación que usan la autenticación previa de Azure Active Directory
- Aplicaciones integradas en la plataforma de aplicaciones de Azure AD que usan la autenticación de OAuth 2.0 u OpenID Connect después de que un usuario o un administrador han dado su consentimiento en esa aplicación.

Cuando se requiere la asignación de usuarios, solo podrán iniciar sesión los usuarios que se asignen expresamente a la aplicación (ya sea a través de una asignación directa de usuarios o según la pertenencia a grupos). Estos pueden acceder a la aplicación desde su página Mis aplicaciones o a través de un vínculo directo. 

Cuando la asignación *no es necesaria*, ya sea porque esta opción se ha establecido en **No** o porque la aplicación usa otro modo de SSO, podrá acceder a la aplicación cualquier usuario que tenga un vínculo directo a la aplicación o la **dirección URL de acceso de usuario** en la página **Propiedades** de la aplicación. 

Esto no afecta a si una aplicación aparece o no en el panel de acceso Mis aplicaciones. Las aplicaciones aparecen en los paneles de acceso Mis aplicaciones de los usuarios en el momento en que un usuario o un grupo se asigna a la aplicación en cuestión. Para obtener información general, vea [Administración del acceso a las aplicaciones](what-is-access-management.md).


Para requerir la asignación de usuarios en una aplicación:

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta de administrador o como propietario de la aplicación.

2. Seleccione **Azure Active Directory**. En el menú de navegación de la izquierda, seleccione **Aplicaciones empresariales**.

3. Seleccione la aplicación de la lista. Si no la ve, empiece a escribir su nombre en el cuadro de búsqueda. También puede usar controles de filtro para seleccionar el tipo de aplicación, el estado o la visibilidad. Tras ello, seleccione **Aplicar**.

4. En el menú de navegación de la izquierda, seleccione **Propiedades**.

5. Asegúrese de que el botón de alternancia **¿Asignación de usuarios?** está establecido en **Sí**.

   > [!NOTE]
   > Si **¿Asignación de usuarios?** no está disponible, puede usar PowerShell para establecer la propiedad appRoleAssignmentRequired en la entidad de servicio.

6. Seleccione el botón **Guardar** de la parte superior de la pantalla.

## <a name="assign-users-or-groups-to-an-app-via-the-azure-portal"></a>Asignación de usuarios o grupos a una aplicación en Azure Portal

1. Inicie sesión en [Azure Portal](https://portal.azure.com) como un administrador global, un administrador de aplicaciones o un administrador de aplicaciones en la nube, o bien como el propietario de la aplicación empresarial.
2. Seleccione **Azure Active Directory**. En el menú de navegación de la izquierda, seleccione **Aplicaciones empresariales**.
3. Seleccione la aplicación de la lista. Si no la ve, empiece a escribir su nombre en el cuadro de búsqueda. También puede usar controles de filtro para seleccionar el tipo de aplicación, el estado o la visibilidad. Tras ello, seleccione **Aplicar**.
4. En el menú de navegación de la izquierda, seleccione **Usuarios y grupos**.
   > [!NOTE]
   > Si quiere asignar usuarios a aplicaciones de Microsoft como aplicaciones de Office 365, algunas de estas aplicaciones usan PowerShell. 
5. Seleccione el botón **Agregar usuario**.
6. En el panel **Agregar asignación**, seleccione **Usuarios y grupos**.
7. Seleccione el usuario o grupo que quiera asignar a la aplicación o empiece a escribir el nombre del usuario o grupo en el cuadro de búsqueda. Puede elegir varios usuarios y grupos; sus selecciones aparecerán en **Elementos seleccionados**.
8. Cuando termine, haga clic en **Guardar**.

   ![Asignación de un usuario o un grupo a la aplicación](./media/assign-user-or-group-access-portal/assign-users.png)

9. En el panel **Usuarios y grupos**, seleccione uno o varios usuarios o grupos de la lista y, luego, haga clic en el botón **Seleccionar** en la parte inferior del panel.
10. Si la aplicación lo permite, puede asignar un rol al usuario o al grupo. En el panel **Agregar asignación**, elija **Seleccionar rol**. Después, en el panel **Seleccionar rol**, seleccione el rol que quiera aplicar a los usuarios o grupos escogidos y, luego, haga clic en **Aceptar** en la parte inferior del panel. 

    > [!NOTE]
    > Si la aplicación no permite seleccionar roles, se asignará el rol de acceso predeterminado. En este caso, la aplicación administrará el nivel de acceso que tienen los usuarios.

2. En el panel **Agregar asignación**, haga clic en el botón **Asignar** en la parte inferior del panel.

## <a name="assign-users-or-groups-to-an-app-via-powershell"></a>Asignación de usuarios o grupos a una aplicación con PowerShell

1. Abra un símbolo del sistema de Windows PowerShell con privilegios elevados.

   > [!NOTE]
   > Debe instalar el módulo de AzureAD (use el comando `Install-Module -Name AzureAD`). Si se le pide que instale un módulo de NuGet o el nuevo módulo de PowerShell para Azure Active Directory V2, escriba S y presione ENTRAR.

1. Ejecute `Connect-AzureAD` e inicie sesión con una cuenta de usuario administrador global.
1. Use el siguiente script para asignar un usuario y un rol a una aplicación:

    ```powershell
    # Assign the values to the variables
    $username = "<You user's UPN>"
    $app_name = "<Your App's display name>"
    $app_role_name = "<App role display name>"

    # Get the user to assign, and the service principal for the app to assign to
    $user = Get-AzureADUser -ObjectId "$username"
    $sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }

    # Assign the user to the app role
    New-AzureADUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```

Para obtener más información sobre cómo asignar un usuario a un rol de aplicación, consulte la documentación de [New-AzureADUserAppRoleAssignment](https://docs.microsoft.com/powershell/module/azuread/new-azureaduserapproleassignment?view=azureadps-2.0).

Para asignar un grupo a una aplicación empresarial, es necesario reemplazar `Get-AzureADUser` por `Get-AzureADGroup` y reemplazar `New-AzureADUserAppRoleAssignment` por `New-AzureADGroupAppRoleAssignment`.

Para obtener más información sobre cómo asignar un grupo a un rol de aplicación, consulte la documentación de [New-AzureADGroupAppRoleAssignment](https://docs.microsoft.com/powershell/module/azuread/new-azureadgroupapproleassignment?view=azureadps-2.0).

### <a name="example"></a>Ejemplo

En este ejemplo se asigna el usuario Britta Simon a la aplicación [Microsoft Workplace Analytics](https://products.office.com/business/workplace-analytics) mediante PowerShell.

1. En PowerShell, asigne los valores correspondientes a las variables $username, app_name $ y $app_role_name.

    ```powershell
    # Assign the values to the variables
    $username = "britta.simon@contoso.com"
    $app_name = "Workplace Analytics"
    ```

1. En este ejemplo, no se sabe cuál es el nombre exacto del rol de aplicación que se quiere asignar a Britta Simon. Ejecute los comandos siguientes para obtener el usuario ($user) y la entidad de servicio ($sp) mediante el UPN de usuario y los nombres para mostrar de la entidad de servicio.

    ```powershell
    # Get the user to assign, and the service principal for the app to assign to
    $user = Get-AzureADUser -ObjectId "$username"
    $sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"
    ```

1. Ejecute el comando `$sp.AppRoles` para mostrar los roles disponibles para la aplicación Workplace Analytics. En este ejemplo, queremos asignar a Britta Simon el rol de Analyst (acceso limitado).

   ![Muestra los roles disponibles para un usuario con el rol Workplace Analytics.](./media/assign-user-or-group-access-portal/workplace-analytics-role.png)

1. Asigne el nombre de rol a la variable `$app_role_name`.

    ```powershell
    # Assign the values to the variables
    $app_role_name = "Analyst (Limited access)"
    $appRole = $sp.AppRoles | Where-Object { $_.DisplayName -eq $app_role_name }
    ```

1. Ejecute el comando siguiente para asignar el rol de aplicación al usuario:

    ```powershell
    # Assign the user to the app role
    New-AzureADUserAppRoleAssignment -ObjectId $user.ObjectId -PrincipalId $user.ObjectId -ResourceId $sp.ObjectId -Id $appRole.Id
    ```

## <a name="related-articles"></a>Artículos relacionados

- [Más información sobre el acceso de los usuarios finales a las aplicaciones](end-user-experiences.md)
- [Planeamiento de la implementación del Panel de acceso de Azure AD](access-panel-deployment-plan.md)
- [Administración del acceso a las aplicaciones](what-is-access-management.md)
 
## <a name="next-steps"></a>Pasos siguientes

- [Ver todos mis grupos](../fundamentals/active-directory-groups-view-azure-portal.md)
- [Quitar una asignación de usuario o grupo de una aplicación empresarial](remove-user-or-group-access-portal.md)
- [Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial](disable-user-sign-in-portal.md)
- [Cambio del nombre o el logotipo de una aplicación empresarial](change-name-or-logo-portal.md)
