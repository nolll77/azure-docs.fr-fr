---
title: 'Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Keeper Password Manager & Digital Vault.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/07/2020
ms.author: jeedes
ms.openlocfilehash: 05b81457af8e74f95bdd3af940fa2b39ba93504a
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92459139"
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a>Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault

Dans ce didacticiel, vous allez apprendre à intégrer Keeper Password Manager & Digital Vault à Azure Active Directory (Azure AD).
L’intégration de Keeper Password Manager & Digital Vault à Azure AD vous offre les avantages suivants :

* Dans Azure AD, vous pouvez contrôler qui a accès à Keeper Password Manager & Digital Vault.
* Vous pouvez permettre aux utilisateurs de se connecter automatiquement à Keeper Password Manager & Digital Vault (via l’authentification unique) avec leur compte Azure AD.
* Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).
Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>Conditions préalables requises

Pour configurer l’intégration d’Azure AD à Keeper Password Manager & Digital Vault, vous avez besoin des éléments suivants :

* Un abonnement Azure AD Si vous n’avez pas d’environnement Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).
* Abonnement Keeper Password Manager & Digital Vault pour lequel l’authentification unique est activée

## <a name="scenario-description"></a>Description du scénario

Dans ce didacticiel, vous configurez et testez l’authentification unique Azure AD dans un environnement de test.

* Keeper Password Manager & Digital Vault prend en charge l’authentification unique initiée par le **fournisseur de services**

* Keeper Password Manager & Digital Vault prend en charge l’attribution d’utilisateurs **juste-à-temps**

* Une fois que vous avez configuré Keeper Password Manager & Digital Vault, vous pouvez appliquer le contrôle de session, qui protège l’exfiltration et l’infiltration des données sensibles de votre organisation en temps réel. Le contrôle de session est étendu à partir de l’accès conditionnel. [Découvrir comment appliquer un contrôle de session avec Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad)

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a>Ajout de Keeper Password Manager & Digital Vault à partir de la galerie

Pour configurer l’intégration de Keeper Password Manager & Digital Vault à Azure AD, vous devez ajouter Keeper Password Manager & Digital Vault à partir de la galerie à votre liste d’applications SaaS gérées.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte professionnel ou scolaire ou avec un compte personnel Microsoft.
1. Dans le panneau de navigation gauche, sélectionnez le service **Azure Active Directory** .
1. Accédez à **Applications d’entreprise** , puis sélectionnez **Toutes les applications** .
1. Pour ajouter une nouvelle application, sélectionnez **Nouvelle application** .
1. Dans la section **Ajouter à partir de la galerie** , tapez **Keeper Password Manager & Digital Vault** dans la zone de recherche.
1. Sélectionnez **Keeper Password Manager & Digital Vault** dans le volet des résultats, puis ajoutez l’application. Patientez quelques secondes pendant que l’application est ajoutée à votre locataire.

## <a name="configure-and-test-azure-ad-sso-for-keeper-password-manager--digital-vault"></a>Configurer et tester l’authentification unique Azure AD pour Keeper Password Manager & Digital Vault

Configurez et testez l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault à l’aide d’un utilisateur de test appelé **B.Simon** . Pour que l’authentification unique fonctionne, vous devez établir une relation entre un utilisateur Azure AD et l’utilisateur associé dans Keeper Password Manager & Digital Vault.

Pour configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault, effectuez les modules suivants :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-sso)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.

    * **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
    * **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.

1. **[Configurer l’authentification unique Keeper Password Manager & Digital Vault](#configure-keeper-password-manager--digital-vault-sso)** pour configurer les paramètres d’authentification unique côté application.
    * **[Créer un utilisateur de test Keeper Password Manager & Digital Vault](#create-keeper-password-manager--digital-vault-test-user)** pour avoir un équivalent de Britta Simon dans Keeper Password Manager & Digital Vault lié à la représentation Azure AD associée.
1. **[Tester l’authentification unique](#test-sso)** pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Effectuez les étapes suivantes pour activer l’authentification unique Azure AD dans le Portail Azure.

1. Sur le [portail Azure](https://portal.azure.com/), dans la page d’intégration de l’application **Keeper Password Manager & Digital Vault** , recherchez la section **Gérer** , puis sélectionnez **Authentification unique** .
1. Dans la page **Sélectionner une méthode d’authentification unique** , sélectionnez **SAML** .
1. Dans la page **Configurer l’authentification unique avec SAML** , cliquez sur l’icône de modification/stylet de **Configuration SAML de base** pour modifier les paramètres.

   ![Modifier la configuration SAML de base](common/edit-urls.png)

4. Dans la section **Configuration SAML de base** , effectuez les étapes suivantes :

    a. Dans la zone de texte **URL de connexion** , saisissez une URL au format suivant : 
    * Pour l’ **authentification unique cloud**  : `https://keepersecurity.com/api/rest/sso/saml/sso/<CLOUD_INSTANCE_ID>`
    * Pour l’ **authentification unique locale**  : `https://<KEEPER_FQDN>/sso-connect/saml/login`

    b. Dans la zone de texte **Identificateur (ID d’entité)** , saisissez une URL au format suivant :
    * Pour l’ **authentification unique cloud**  : `https://keepersecurity.com/api/rest/sso/saml/<CLOUD_INSTANCE_ID>`
    * Pour l’ **authentification unique locale**  : `https://<KEEPER_FQDN>/sso-connect`

    c. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : 
    * Pour l’ **authentification unique cloud**  : `https://keepersecurity.com/api/rest/sso/saml/sso/<CLOUD_INSTANCE_ID>`
    * Pour l’ **authentification unique locale**  : `https://<KEEPER_FQDN>/sso-connect/saml/sso`

    > [!NOTE]
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion, l’identificateur et l’URL de réponse réels. Pour obtenir ces valeurs, contactez [l’équipe de support technique de Keeper Password Manager & Digital Vault](https://keepersecurity.com/contact.html). Vous pouvez également consulter les modèles figurant à la section **Configuration SAML de base** dans le portail Azure.

5. Sur la page **Configurer l’authentification unique avec SAML** , dans la section **Certificat de signature SAML** , cliquez sur **Télécharger** pour télécharger le fichier **XML de métadonnées de fédération** en fonction des options définies selon vos besoins, puis enregistrez-le sur votre ordinateur.

    ![Lien Téléchargement de certificat](common/metadataxml.png)

6. Dans la section **Configurer Keeper Password Manager & Digital Vault** , copiez la ou les URL appropriées correspondant à vos besoins.

    ![Copier les URL de configuration](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD 

Dans cette section, vous allez créer un utilisateur de test appelé B. Simon dans le portail Azure.

1. Dans le volet gauche du Portail Azure, sélectionnez **Azure Active Directory** , **Utilisateurs** , puis **Tous les utilisateurs** .
1. Sélectionnez **Nouvel utilisateur** dans la partie supérieure de l’écran.
1. Dans les propriétés **Utilisateur** , effectuez les étapes suivantes :
   1. Dans le champ **Nom** , entrez `B.Simon`.  
   1. Dans le champ **Nom de l’utilisateur** , entrez username@companydomain.extension. Par exemple : `B.Simon@contoso.com`.
   1. Cochez la case **Afficher le mot de passe** , puis notez la valeur affichée dans le champ **Mot de passe** .
   1. Cliquez sur **Créer** .

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser B.Simon à utiliser l’authentification unique Azure en accordant l’accès à Keeper Password Manager & Digital Vault.

1. Dans le portail Azure, sélectionnez **Applications d’entreprise** , puis **Toutes les applications** .
1. Dans la liste des applications, sélectionnez **Keeper Password Manager & Digital Vault** .
1. Dans la page de vue d’ensemble de l’application, recherchez la section **Gérer** et sélectionnez **Utilisateurs et groupes** .

   ![Lien « Utilisateurs et groupes »](common/users-groups-blade.png)

1. Sélectionnez **Ajouter un utilisateur** , puis **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une attribution** .

    ![Lien Ajouter un utilisateur](common/add-assign-user.png)

1. Dans la boîte de dialogue **Utilisateurs et groupes** , sélectionnez **B. Simon** dans la liste Utilisateurs, puis cliquez sur le bouton **Sélectionner** au bas de l’écran.
1. Si vous attendez une valeur de rôle dans l’assertion SAML, dans la boîte de dialogue **Sélectionner un rôle** , sélectionnez le rôle approprié pour l’utilisateur dans la liste, puis cliquez sur le bouton **Sélectionner** en bas de l’écran.
1. Dans la boîte de dialogue **Ajouter une attribution** , cliquez sur le bouton **Attribuer** .


## <a name="configure-keeper-password-manager--digital-vault-sso"></a>Configurer l’authentification unique Keeper Password Manager & Digital Vault

Pour configurer l’authentification unique côté **Keeper Password Manager & Digital Vault** , suivez les instructions fournies dans le [guide de prise en charge de Keeper](https://docs.keeper.io/sso-connect-guide/).

### <a name="create-keeper-password-manager--digital-vault-test-user"></a>Créer un utilisateur de test Keeper Password Manager & Digital Vault

Pour se connecter à Keeper Password Manager & Digital Vault, les utilisateurs d’Azure AD doivent être approvisionnés dans Keeper Password Manager & Digital Vault. L’application prend en charge la configuration d’utilisateur juste à temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application. Si vous voulez configurer des utilisateurs manuellement, vous pouvez contacter le [support de Keeper](https://keepersecurity.com/contact.html).

## <a name="test-sso"></a>Tester l’authentification unique (SSO)

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette Keeper Password Manager & Digital Vault dans le volet d’accès, vous devez être automatiquement connecté à l’application Keeper Password Manager & Digital Vault pour laquelle vous avez configuré l’authentification unique. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Ressources supplémentaires

- [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](./tutorial-list.md)

- [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

- [Qu’est-ce que l’accès conditionnel dans Azure Active Directory ?](../conditional-access/overview.md)

- [Essayer Keeper Password Manager & Digital Vault avec Azure AD](https://aad.portal.azure.com/)

- [Qu’est-ce que le contrôle de session dans Microsoft Cloud App Security ?](/cloud-app-security/proxy-intro-aad)