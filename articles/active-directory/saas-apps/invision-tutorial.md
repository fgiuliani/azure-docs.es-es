---
title: 'Tutorial: Integración del inicio de sesión único (SSO) de Azure Active Directory con InVision | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory e InVision.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 02487206-30b0-4b1d-ae99-573c3d2ef9b0
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 04/09/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c2427fff37158745e416f4b2f0641697ad62ea9
ms.sourcegitcommit: acb82fc770128234f2e9222939826e3ade3a2a28
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81682692"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-invision"></a>Tutorial: Integración del inicio de sesión único (SSO) de Azure Active Directory con InVision

En este tutorial, obtendrá información sobre cómo integrar InVision con Azure Active Directory (Azure AD). Al integrar InVision con Azure AD, puede hacer lo siguiente:

* Controlar en Azure AD quién tiene acceso a InVision.
* Permitir que los usuarios puedan iniciar sesión automáticamente en InVision con sus cuentas de Azure AD.
* Administrar las cuentas desde una ubicación central (Azure Portal).

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on)

## <a name="prerequisites"></a>Prerrequisitos

Para empezar, necesita los siguientes elementos:

* Una suscripción de Azure AD. Si no tiene una suscripción, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/).
* Una suscripción habilitada para el inicio de sesión único (SSO) en InVision.

## <a name="scenario-description"></a>Descripción del escenario

En este tutorial, va a configurar y probar el inicio de sesión único de Azure AD en un entorno de prueba.

* InVision admite el inicio de sesión único iniciado por **SP e IDP**.
* Una vez configurado InVision, puede aplicar el control de sesión, que protege la filtración y la infiltración de la información confidencial de la organización en tiempo real. El control de sesión procede del acceso condicional. [Aprenda a aplicar el control de sesión con Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-invision-from-the-gallery"></a>Adición de InVision desde la galería

Para configurar la integración de InVision en Azure AD, debe agregar InVision desde la galería a la lista de aplicaciones SaaS administradas.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta personal, profesional o educativa de Microsoft.
1. En el panel de navegación de la izquierda, seleccione el servicio **Azure Active Directory**.
1. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.
1. Para agregar una nueva aplicación, seleccione **Nueva aplicación**.
1. En la sección **Agregar desde la galería**, escriba **InVision** en el cuadro de búsqueda.
1. Seleccione **InVision** en el panel de resultados y agregue la aplicación. Espere unos segundos mientras la aplicación se agrega al inquilino.

## <a name="configure-and-test-azure-ad-single-sign-on-for-invision"></a>Configuración y prueba del inicio de sesión único de Azure AD para InVision

Configure y pruebe el inicio de sesión único de Azure AD con InVision mediante un usuario de prueba llamado **B.Simon**. Para que el inicio de sesión único funcione, es preciso establecer una relación de vinculación entre un usuario de Azure AD y el usuario correspondiente de InVision.

Para configurar y probar el inicio de sesión único de Azure AD con InVision, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-sso)** , para permitir que los usuarios puedan utilizar esta característica.
    * **[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)** , para probar el inicio de sesión único de Azure AD con B.Simon.
    * **[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)** , para habilitar a B.Simon para que use el inicio de sesión único de Azure AD.
1. **[Configuración del inicio de sesión único en InVision](#configure-invision-sso)** : para configurar los valores de inicio de sesión único en la aplicación.
    * **[Creación de un usuario de prueba de InVision](#create-invision-test-user)** : para tener un homólogo de B.Simon en InVision vinculado a la representación del usuario en Azure AD.
1. **[Prueba del inicio de sesión único](#test-sso)** : para comprobar si la configuración funciona.

## <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

Siga estos pasos para habilitar el inicio de sesión único de Azure AD en Azure Portal.

1. En [Azure Portal](https://portal.azure.com/), en la página de integración de aplicaciones de **InVision**, busque la sección **Administrar** y seleccione **Inicio de sesión único**.
1. En la página **Seleccione un método de inicio de sesión único**, elija **SAML**.
1. En la página **Configurar el inicio de sesión único con SAML**, haga clic en el icono de edición o con forma de lápiz para abrir el cuadro de diálogo **Configuración básica de SAML** y modificar la configuración.

   ![Edición de la configuración básica de SAML](common/edit-urls.png)

1. En la sección **Configuración básica de SAML**, si desea configurar la aplicación en modo iniciado por **IDP**, escriba los valores de los siguientes campos:

    a. En el cuadro de texto **Identificador**, escriba una dirección URL con el patrón siguiente: `https://<SUBDOMAIN>.invisionapp.com`

    b. En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<SUBDOMAIN>.invisionapp.com//sso/auth`

1. Haga clic en **Establecer direcciones URL adicionales** y siga este paso si desea configurar la aplicación en el modo iniciado por **SP**:

    En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<SUBDOMAIN>.invisionapp.com`

    > [!NOTE]
    > Estos valores no son reales. Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión. Póngase en contacto con el [equipo de soporte técnico de InVision](mailto:support@invisionapp.com) para obtener estos valores. También puede hacer referencia a los patrones que se muestran en la sección **Configuración básica de SAML** de Azure Portal.

1. En la página **Configurar el inicio de sesión único con SAML**, en la sección **Certificado de firma de SAML**, busque **Certificado (Base64)** y seleccione **Descargar** para descargarlo y guardarlo en el equipo.

    ![Vínculo de descarga del certificado](common/certificatebase64.png)

1. En la sección **Configurar InVision**, copie las direcciones URL adecuadas según sus necesidades.

    ![Copiar direcciones URL de configuración](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

En esta sección, va a crear un usuario de prueba llamado B.Simon en Azure Portal.

1. En el panel izquierdo de Azure Portal, seleccione **Azure Active Directory**, **Usuarios** y **Todos los usuarios**.
1. Seleccione **Nuevo usuario** en la parte superior de la pantalla.
1. En las propiedades del **usuario**, siga estos pasos:
   1. En el campo **Nombre**, escriba `B.Simon`.  
   1. En el campo **Nombre de usuario**, escriba username@companydomain.extension. Por ejemplo, `B.Simon@contoso.com`.
   1. Active la casilla **Show password** (Mostrar contraseña) y, después, anote el valor que se muestra en el cuadro **Contraseña**.
   1. Haga clic en **Crear**.

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, va a permitir que B.Simon acceda a InVision mediante el inicio de sesión único de Azure.

1. En Azure Portal, seleccione sucesivamente **Aplicaciones empresariales** y **Todas las aplicaciones**.
1. En la lista de aplicaciones, seleccione **InVision**.
1. En la página de información general de la aplicación, busque la sección **Administrar** y seleccione **Usuarios y grupos**.

   ![Vínculo "Usuarios y grupos"](common/users-groups-blade.png)

1. Seleccione **Agregar usuario**. A continuación, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.

    ![Vínculo de Agregar usuario](common/add-assign-user.png)

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **B.Simon** de la lista de usuarios y haga clic en el botón **Seleccionar** de la parte inferior de la pantalla.
1. Si espera que haya un valor de rol en la aserción de SAML, en el cuadro de diálogo **Seleccionar rol**, seleccione en la lista el rol adecuado para el usuario y haga clic en el botón **Seleccionar** en la parte inferior de la pantalla.
1. En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.

## <a name="configure-invision-sso"></a>Configuración del inicio de sesión único de InVision

1. En otra ventana del explorador web, inicie sesión en el sitio web de InVision como administrador.

1. Haga clic en **Team** (Equipo) y seleccione **Settings** (Configuración).

    ![Configuración de InVision](./media/invision-tutorial/config1.png)

1. Desplácese hacia abajo hasta **Single sign-on**(Inicio de sesión único) y, a continuación, haga clic en **Change** (Cambiar).

    ![Configuración de InVision](./media/invision-tutorial/config3.png)

1. En la página **Single sign-on** (Inicio de sesión único) realice los pasos siguientes:

    ![Configuración de InVision](./media/invision-tutorial/config4.png)

    a. Cambie **Require SSO for every member of < account name >** (Requerir SSO para cada miembro de <nombre de cuenta>) a **On** (Activado).

    b. En el cuadro de texto **Name** (Nombre), escriba el nombre; por ejemplo, `azureadsso`.

    c. Escriba el valor de la dirección URL de inicio de sesión en el cuadro de texto **Sign-in URL** (Dirección URL de inicio de sesión).

    d. En el cuadro de texto **Sign-out URL** (Dirección URL de cierre de sesión), pegue el valor de **Dirección URL de cierre de sesión** que ha copiado de Azure Portal.

    e. En el cuadro de texto **SAML Certificate** (Certificado de SAML), abra el archivo **Certificado (base 64)** descargado en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto SAML Certificate (Certificado de SAML).

    f. En el cuadro de texto **Name ID Format** (Formato del identificador de nombre), use `Unspecified` para el campo **Name ID Format** (Formato del identificador de nombre).

    g. Seleccione **SHA-256** en la lista desplegable **HASH Algorithm** (Algoritmo hash).

    h. Escriba el nombre adecuado para **SSO Button Label** (Etiqueta del botón de SSO).

    i. Cambie **Allow Just-in-Time provisioning** (Permitir aprovisionamiento Just-In-Time) a On (Activado).

    j. Haga clic en **Update**(Actualizar).

### <a name="create-invision-test-user"></a>Creación de un usuario de prueba de InVision

1. En otra ventana del explorador web, inicie sesión en el sitio web de InVision como administrador.

1. Haga clic en **Team** (Equipo) y seleccione **People** (Personas).

    ![Configuración de InVision](./media/invision-tutorial/config2.png)

1. Haga clic en el **icono +** para agregar un nuevo usuario.

    ![Configuración de InVision](./media/invision-tutorial/user1.png)

1. Escriba la dirección de correo electrónico del usuario y haga clic en **Next** (Siguiente).

    ![Configuración de InVision](./media/invision-tutorial/user2.png)

1. Confirme la dirección de correo electrónico y haga clic en **Invite** (Invitar).

    ![Configuración de InVision](./media/invision-tutorial/user3.png)

## <a name="test-sso"></a>Prueba de SSO

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de InVision en el panel de acceso, debería iniciar sesión automáticamente en la instancia de InVision para la que configuró el inicio de sesión único. Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos adicionales

- [Lista de tutoriales acerca de cómo integrar aplicaciones SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [¿Qué es el acceso a las aplicaciones y el inicio de sesión único con Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on)

- [¿Qué es el acceso condicional en Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Prueba de InVision con Azure AD](https://aad.portal.azure.com/)

- [¿Qué es el control de sesiones en Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)

- [Protección de InVision con controles y visibilidad avanzados](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)