---
title: Nouveautés Notes de publication - Azure Active Directory | Microsoft Docs
description: Découvrez les nouveautés d’Azure Active Directory, notamment les dernières notes de publication, les problèmes connus, les corrections de bogues, les fonctionnalités déconseillées et les modifications à venir.
services: active-directory
author: ajburnle
manager: daveba
featureFlags:
- clicktale
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.subservice: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 10/06/2020
ms.author: ajburnle
ms.reviewer: dhanyahk
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dc60fd14eb26ab4c8f5a867b97369a066b743b
ms.sourcegitcommit: 28c5fdc3828316f45f7c20fc4de4b2c05a1c5548
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92362754"
---
# <a name="whats-new-in-azure-active-directory"></a>Nouveautés d’Azure Active Directory

>Soyez notifié de la disponibilité des mises à jour sur cette page en faisant un copier-coller de cette URL : `https://docs.microsoft.com/api/search/rss?search=%22Release+notes+-+Azure+Active+Directory%22&locale=en-us` dans votre lecteur de flux ![icône RSS](./media/whats-new/feed-icon-16x16.png).

Azure AD bénéficie d’améliorations en continu. Pour vous informer des développements les plus récents, cet article détaille les thèmes suivants :

- Versions les plus récentes
- Problèmes connus
- Résolution des bogues
- Fonctionnalités dépréciées
- Modifications planifiées

Cette page est mise à jour tous les mois. Donc, consultez-la régulièrement. Si vous recherchez des éléments antérieurs aux six derniers mois, vous les trouverez dans l’[Archive des Nouveautés d’Azure Active Directory](whats-new-archive.md).

---

## <a name="september-2020"></a>Septembre 2020

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---september-2020"></a>Nouveaux connecteurs de provisionnement dans la galerie d’applications Azure AD - Septembre 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Intégration tierce
 
Vous pouvez désormais automatiser la création, la mise à jour et la suppression de comptes d’utilisateur pour ces applications nouvellement intégrées :

- [Coda](../saas-apps/coda-provisioning-tutorial.md)
- [Cofense Recipient Sync](../saas-apps/cofense-provision-tutorial.md)
- [InVision](../saas-apps/invision-provisioning-tutorial.md)
- [myday](../saas-apps/myday-provision-tutorial.md)
- [SAP Analytics Cloud](../saas-apps/sap-analytics-cloud-provisioning-tutorial.md)
- [Webroot Security Awareness](../saas-apps/webroot-security-awareness-training-provisioning-tutorial.md)

Pour découvrir comment sécuriser plus efficacement votre organisation à l’aide de l’approvisionnement automatique de comptes utilisateur, voir [Automatisation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure AD](../app-provisioning/user-provisioning.md).
 
---
### <a name="cloud-provisioning-public-preview-refresh"></a>Actualisation de la préversion publique de provisionnement cloud

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement cloud Azure AD **Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
L’actualisation de la préversion publique de provisionnement cloud Azure AD Connect propose deux améliorations majeures développées à partir des commentaires des clients : 

- Expérience de mappage d’attributs par le biais du portail Azure

    Avec cette fonctionnalité, les administrateurs informatiques peuvent mapper des attributs d’utilisateur, de groupe ou de contact entre Active Directory et Azure AD à l’aide de différents types de mappage présents aujourd’hui. Le mappage d’attributs est une fonctionnalité utilisée pour standardiser les valeurs des attributs qui circulent d’Active Directory vers Azure Active Directory. Vous pouvez déterminer s’il faut mapper la valeur d’attribut telle quelle d’Active Directory vers Azure AD, ou utiliser des expressions pour transformer les valeurs d’attributs lors du provisionnement des utilisateurs. [En savoir plus](../cloud-provisioning/how-to-attribute-mapping.md)

- Provisionnement à la demande ou expérience de test utilisateur

    Une fois que vous avez paramétré votre configuration, vous souhaiterez peut-être effectuer un test pour voir si la transformation utilisateur fonctionne comme prévu avant de l’appliquer à tous les utilisateurs dans l’étendue. Avec le provisionnement à la demande, les administrateurs informatiques peuvent entrer le nom unique d’un utilisateur Active Directory et voir si la synchronisation fonctionne comme prévu. Le provisionnement à la demande offre un excellent moyen de s’assurer que les mappages d’attributs que vous avez effectués auparavant fonctionnent comme prévu. [En savoir plus](../cloud-provisioning/how-to-on-demand-provision.md)
 
---

### <a name="audited-bitlocker-recovery-in-azure-ad---public-preview"></a>Récupération BitLocker auditée dans Azure AD - Préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Gestion de l’accès aux appareils  
**Fonctionnalité de produit :** Gestion du cycle de vie des appareils
 
Lorsque des administrateurs informatiques ou des utilisateurs finaux lisent des clés de récupération BitLocker auxquelles ils ont accès, Azure Active Directory génère désormais un journal d’audit qui capture les utilisateurs ayant accédé à la clé de récupération. Le même audit fournit des détails sur l’appareil auquel la clé BitLocker a été associée.

Les utilisateurs finaux peuvent [accéder à leurs clés de récupération par le biais de Mon compte](../user-help/my-account-portal-devices-page.md#view-a-bitlocker-key). Les administrateurs informatiques peuvent accéder aux clés de récupération par le biais de l’[API de clé de récupération BitLocker en version bêta](/graph/api/resources/bitlockerrecoverykey?view=graph-rest-beta) ou du portail Azure AD. Pour plus d’informations, consultez [Afficher ou copier des clés BitLocker dans le portail Azure AD](../devices/device-management-azure-portal.md#view-or-copy-bitlocker-keys).

---

### <a name="teams-devices-administrator-built-in-role"></a>Rôle intégré Administrateur d’appareils Teams

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** RBAC  
**Fonctionnalité de produit :** Contrôle d’accès
 
Les utilisateurs détenant rôle [Administrateur d’appareils Teams](../roles/permissions-reference.md#teams-devices-administrator) peuvent gérer des [appareils certifiés par Teams](https://www.microsoft.com/microsoft-365/microsoft-teams/across-devices/devices) à partir du Centre d’administration Teams. 

Ce rôle permet à l’utilisateur d’afficher tous les appareils en un seul coup d’œil, avec la possibilité de rechercher et de filtrer les appareils. L’utilisateur peut également vérifier les détails de chaque appareil, notamment le compte de connexion, la marque et le modèle de l’appareil. L’utilisateur peut modifier les paramètres sur l’appareil et mettre à jour les versions des logiciels. Ce rôle n’accorde pas d’autorisations pour vérifier l’activité Teams et la qualité d’appel de l’appareil.
 
---

### <a name="advanced-query-capabilities-for-directory-objects"></a>Fonctionnalités de requête avancées pour les objets d’annuaire

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** MS Graph  
**Fonctionnalité de produit :** Expérience de développement
 
Toutes les nouvelles fonctionnalités de requête introduites pour les objets d’annuaire dans les API Azure AD sont désormais disponibles dans le point de terminaison v1.0 et prêtes pour la production. Les développeurs peuvent compter, rechercher, filtrer et trier les objets d’annuaire et les liens connexes à l’aide des opérateurs OData standard.

Pour plus d’informations, reportez-vous à la documentation [ici](https://aka.ms/BlogPostMezzoGA). Vous pouvez également envoyer vos commentaires à l’aide de cette [brève enquête](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_yN8EPoGo5OpR1hgmCp1XxUMENJRkNQTk5RQkpWTE44NEk2U0RIV0VZRy4u).
 
---

### <a name="public-preview-continuous-access-evaluation-for-tenants-who-configured-conditional-access-policies"></a>Préversion publique : évaluation continue de l’accès pour les locataires qui ont configuré des stratégies d’accès conditionnel

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
L’évaluation continue de l’accès est désormais disponible en préversion publique pour les locataires Azure AD ayant des stratégies d’accès conditionnel. Avec elle, les stratégies et les événements de sécurité critiques sont évalués en temps réel. Cela comprend la désactivation du compte, la réinitialisation du mot de passe et la modification de l’emplacement. Pour plus d’informations, consultez [Évaluation continue de l’accès](../conditional-access/concept-continuous-access-evaluation.md).

---

### <a name="public-preview-ask-users-requesting-an-access-package-additional-questions-to-improve-approval-decisions"></a>Préversion publique : poser aux utilisateurs qui demandent un package d’accès des questions supplémentaires afin d’améliorer les décisions d’approbation

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Gestion de l’accès utilisateur  
**Fonctionnalité de produit :** Gestion des droits d’utilisation
 
Les administrateurs peuvent désormais exiger que les utilisateurs qui demandent un package d’accès répondent à des questions supplémentaires au-delà de la justification commerciale dans le portail Mon Accès de gestion des droits d’utilisation Azure AD. Les réponses des utilisateurs sont ensuite présentées aux approbateurs afin de les aider à prendre une décision d’approbation d’accès plus précise. Pour en savoir plus, consultez [Collecter des informations supplémentaires sur le demandeur pour approbation (préversion)](../governance/entitlement-management-access-package-approval-policy.md#collect-additional-requestor-information-for-approval-preview).
 
---

### <a name="public-preview-enhanced-user-management"></a>Préversion publique : gestion des utilisateurs améliorée

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** User Management  
**Fonctionnalité de produit :** User Management
 

Le portail Azure AD a été mis à jour afin de faciliter la recherche d’utilisateurs dans les pages Tous les utilisateurs et Utilisateurs supprimés. Les modifications apportées à la préversion sont les suivantes : 
- Propriétés utilisateur plus visibles, notamment l’ID d’objet, l’état de synchronisation d’annuaire, le type de création et l’émetteur d’identité.
- La fonctionnalité de recherche autorise désormais la recherche combinée de noms, d’e-mails et d’ID d’objets.
- Filtrage amélioré par type d’utilisateur (membre, invité et aucun), état de la synchronisation d’annuaire, type de création, nom de la société et nom de domaine.
- Nouvelles fonctionnalités de tri sur des propriétés telles que le nom, le nom d’utilisateur principal et la date de suppression.
- Nouveau nombre total d’utilisateurs mis à jour avec les recherches ou les filtres.

Pour plus d’informations, consultez [Améliorations de la gestion des utilisateurs (préversion) dans Azure Active Directory](../enterprise-users/users-search-enhanced.md).

---

### <a name="new-notes-field-for-enterprise-applications"></a>Nouveau champ de notes pour les applications d’entreprise

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise **Fonctionnalité produit :** SSO

Vous pouvez ajouter des notes de texte libres aux applications d’entreprise. Vous pouvez ajouter toute information pertinente qui vous aidera à gérer les applications Sous Applications d’entreprise. Pour plus d’informations, consultez [Démarrage rapide : Configurer les propriétés d’une application dans votre locataire Azure Active Directory (Azure AD)](../manage-apps/add-application-portal-configure.md). 

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---september-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD – Septembre 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** Intégration tierce

En septembre 2020, nous avons ajouté les 34 applications suivantes à notre galerie d’applications avec prise en charge de la fédération :

[VMware Horizon - Unified Access Gateway](), [Pulse Secure PCS](../saas-apps/vmware-horizon-unified-access-gateway-tutorial.md), [Inventory360](../saas-apps/pulse-secure-pcs-tutorial.md), [Frontitude](https://services.enteksystems.de/sso/microsoft/signup), [BookWidgets](https://www.bookwidgets.com/sso/office365), [ZVD_Server](https://zaas.zenmutech.com/user/signin), [HashData for Business](https://hashdata.app/login.xhtml), [SecureLogin](https://securelogin.securelogin.nu/sso/azure/login), [CyberSolutions MAILBASEΣ/CMSS](../saas-apps/cybersolutions-mailbase-tutorial.md), [CyberSolutions CYBERMAILΣ](../saas-apps/cybersolutions-cybermail-tutorial.md), [LimbleCMMS](https://auth.limblecmms.com/), [Glint Inc](../saas-apps/glint-inc-tutorial.md), [zeroheight](../saas-apps/zeroheight-tutorial.md), [Gender Fitness](https://app.genderfitness.com/), [Coeo Portal](https://my.coeo.com/), [Grammarly](../saas-apps/grammarly-tutorial.md), [Fivetran](../saas-apps/fivetran-tutorial.md), [Kumolus](../saas-apps/kumolus-tutorial.md), [RSA Archer Suite](../saas-apps/rsa-archer-suite-tutorial.md), [TeamzSkill](../saas-apps/teamzskill-tutorial.md), [raumfürraum](../saas-apps/raumfurraum-tutorial.md), [Saviynt](../saas-apps/saviynt-tutorial.md), [BizMerlinHR](https://marketplace.bizmerlin.net/bmone/signup), [Mobile Locker](../saas-apps/mobile-locker-tutorial.md), [Zengine](../saas-apps/zengine-tutorial.md), [CloudCADI](https://app.cloudcadi.com/login), [Simfoni Analytics](https://simfonianalytics.com/accounts/microsoft/login/), [Priva Identity & Access Management](https://my.priva.com/), [Nitro Pro](https://www.gonitro.com/nps/product-details/downloads), [Eventfinity](../saas-apps/eventfinity-tutorial.md), [Fexa](../saas-apps/fexa-tutorial.md), [Secured Signing Enterprise Portal](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [Secured Signing Enterprise Portal AAD Setup](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [Wistec Online](https://wisteconline.com/auth/oidc), [Oracle PeopleSoft - Protected by F5 BIG-IP APM](../saas-apps/oracle-peoplesoft-protected-by-f5-big-ip-apm-tutorial.md)

La documentation de toutes ces applications est disponible ici : https://aka.ms/AppsTutorial.

Pour référencer votre application dans la galerie d’applications Azure AD, lisez les informations détaillées ici : https://aka.ms/AzureADAppRequest.

---

### <a name="new-delegation-role-in-azure-ad-entitlement-management-access-package-assignment-manager"></a>Nouveau rôle de délégation dans la gestion des droits d’utilisation Azure AD : Gestionnaire d'attribution de package d'accès

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Gestion de l’accès utilisateur  
**Fonctionnalité de produit :** Gestion des droits d’utilisation
 
Un nouveau rôle Gestionnaire d’attribution de package d’accès a été ajouté dans la gestion des droits d’utilisation Azure AD afin de fournir des autorisations précises pour gérer les attributions. Vous pouvez maintenant déléguer des tâches à un utilisateur détenteur ce rôle, qui peut déléguer la gestion des attributions d’un package d’accès à un dirigeant d’entreprise. Toutefois, un Gestionnaire d’attribution de package d’accès ne peut pas modifier les stratégies de package d’accès ou d’autres propriétés définies par les administrateurs. 

Avec ce nouveau rôle, vous bénéficiez des privilèges minimaux nécessaires pour déléguer la gestion des attributions et conserver le contrôle administratif de toutes les autres configurations de package d’accès. Pour plus d’informations, consultez [Rôles de gestion des droits d’utilisation](../governance/entitlement-management-delegate.md#entitlement-management-roles).
 
---

### <a name="changes-to-privileged-identity-managements-onboarding-flow"></a>Modifications apportées au flux d’intégration de Privileged Identity Management

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Privileged Identity Management  
**Fonctionnalité de produit :** Privileged Identity Management
 
Auparavant, l’intégration à Privileged Identity Management (PIM) nécessitait le consentement de l’utilisateur et un flux d’intégration dans le panneau PIM qui incluait l’inscription dans Azure MFA. Avec la récente intégration de l’expérience PIM dans le panneau de rôles et administrateurs Azure AD, nous supprimons cette expérience. Tout locataire ayant une licence P2 valide sera intégré automatiquement à PIM.

L’intégration à PIM n’a aucun effet indésirable direct sur votre locataire. Vous pouvez vous attendre aux changements suivants :
- Options d’attribution supplémentaires telles que actif/éligible avec heure de début et heure de fin lorsque vous effectuez une attribution dans PIM ou dans le panneau de rôles et administrateurs Azure AD. 
- Mécanismes d’étendue supplémentaires, tels que des unités administratives et des rôles personnalisés, introduits directement dans l’expérience d’attribution. 
- Si vous êtes administrateur général ou administrateur de rôle privilégié, vous commencerez peut-être à recevoir quelques e-mails supplémentaires tels que le résumé hebdomadaire PIM. 
- Vous constaterez peut-être aussi la présence du principal de service ms-pim dans le journal d’audit relatif à l’attribution de rôle. Ce changement attendu ne doit pas avoir d’incidence sur votre flux de travail normal.

 Pour plus d’informations, consultez [Commencer à utiliser Privileged Identity Management](../privileged-identity-management/pim-getting-started.md).

---

### <a name="azure-ad-entitlement-management-the-select-pane-of-access-package-resources-now-shows-by-default-the-resources-currently-in-the-selected-catalog"></a>Gestion des droits d’utilisation Azure AD : le volet Sélectionner des ressources de package d’accès affiche désormais par défaut les ressources actuellement dans le catalogue sélectionné

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Gestion de l’accès utilisateur  
**Fonctionnalité de produit :** Gestion des droits d’utilisation
 

Dans le flux de création de package d’accès, sous l’onglet Rôles des ressources, le comportement du volet Sélectionner change. Actuellement, le comportement par défaut consiste à afficher toutes les ressources qui sont détenues par l’utilisateur et les ressources ajoutées au catalogue sélectionné. 

Cette expérience sera changée de façon à afficher uniquement les ressources actuellement ajoutées dans le catalogue par défaut, afin que les utilisateurs puissent facilement sélectionner des ressources à partir du catalogue. La mise à jour facilitera la découverte des ressources à ajouter aux packages d’accès, et réduira les risques liés à l’ajout par inadvertance de ressources détenues par l’utilisateur qui ne font pas partie du catalogue. Pour plus d’informations, consultez [Créer un package d’accès dans la gestion des droits d’utilisation Azure AD](../governance/entitlement-management-access-package-create.md#resource-roles).
 
---

## <a name="august-2020"></a>Août 2020 
 
### <a name="updates-to-azure-multi-factor-authentication-server-firewall-requirements"></a>Mises à jour de la Configuration requise du pare-feu du serveur Azure Multi-Factor Authentication

**Type :** Modification planifiée  
**Catégorie de service :** MFA  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
À partir du 1er octobre 2020, la configuration requise du pare-feu du serveur Azure MFA exigera des plages d’adresses IP supplémentaires.

Si des règles de pare-feu pour le trafic sortant sont en vigueur au sein de votre organisation, mettez à jour les règles de façon à ce que vos serveurs MFA puissent communiquer avec toutes les plages d’adresses IP nécessaires. Les plages d’adresses IP sont documentées dans [Configuration requise du pare-feu du serveur Azure Multi-Factor Authentication](../authentication/howto-mfaserver-deploy.md#azure-multi-factor-authentication-server-firewall-requirements).

---

### <a name="upcoming-changes-to-user-experience-in-identity-secure-score"></a>Modifications à venir de l’expérience utilisateur dans le score d’identité sécurisée

**Type :** Modification planifiée  
**Catégorie de service :** Protection de l’identité **Fonctionnalité produit :** Protection et sécurité des identités

Nous mettons à jour le portail Score d’identité sécurisée pour l’aligner sur les modifications introduites dans la [nouvelle version](/microsoft-365/security/mtp/microsoft-secure-score-whats-new?view=o365-worldwide) du Niveau de sécurité Microsoft. 

La préversion avec les modifications sera disponible début septembre. Les modifications apportées à la préversion sont les suivantes :
- Le « Score d’identité sécurisée » est renommé « Niveau de sécurité de l’identité » pour l’alignement avec Niveau de sécurité Microsoft
- Points normalisés à l’échelle standard et exprimés en pourcentages au lieu de points

Dans cette préversion, les clients peuvent basculer entre l’expérience existante et la nouvelle expérience. Cette préversion publique sera disponible jusqu’à la fin du mois de novembre 2020. Après la préversion, les clients seront automatiquement dirigés vers la nouvelle expérience utilisateur.

---

### <a name="new-restricted-guest-access-permissions-in-azure-ad---public-preview"></a>Nouvelles autorisations d’accès invité restreintes dans Azure AD – Préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Contrôle d’accès   
**Fonctionnalité de produit :** User Management

Nous avons mis à jour les autorisations au niveau répertoire pour les utilisateurs invités. Ces autorisations permettent aux administrateurs d’imposer des restrictions et contrôles supplémentaires à l’accès utilisateur invité externe. Les administrateurs peuvent désormais ajouter des restrictions à l’accès d’invités externes aux informations d’appartenance et de profil des utilisateurs et des groupes. Grâce à cette fonctionnalité en préversion publique, les clients peuvent gérer l’accès des utilisateurs externes à grande échelle en obfusquant les appartenances de groupe, notamment en empêchant les utilisateurs invités de voir les appartenances des groupes dans lesquels ils se trouvent.

Pour plus d’informations, consultez [Autorisations d’accès invité restreintes](../enterprise-users/users-restrict-guest-permissions.md) et [Autorisations par défaut des utilisateurs](./users-default-permissions.md).
 
---

### <a name="general-availability-of-delta-queries-for-service-principals"></a>Disponibilité générale des requêtes delta pour les principaux de service

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** MS Graph  
**Fonctionnalité de produit :** Expérience de développement
 
La requête delta Microsoft Graph prend désormais en charge le type de ressource dans la version v1.0 :
- Principal de service

Désormais, les clients peuvent suivre efficacement les modifications apportées à ces ressources et le service offre la meilleure solution pour synchroniser les modifications apportées à ces ressources avec un magasin de données local. Pour savoir comment configurer ces ressources dans une requête, consultez [Utiliser des requêtes delta pour suivre les modifications apportées aux données de Microsoft Graph](/graph/delta-query-overview).
 
---

### <a name="general-availability-of-delta-queries-for-oauth2permissiongrant"></a>Disponibilité générale des requêtes Delta pour oAuth2PermissionGrant

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** MS Graph  
**Fonctionnalité de produit :** Expérience de développement

La requête delta Microsoft Graph prend désormais en charge le type de ressource dans la version v1.0 :
- OAuth2PermissionGrant

Les clients peuvent désormais suivre efficacement les modifications apportées à ces ressources et le service offre la meilleure solution pour synchroniser les modifications apportées à ces ressources avec un magasin de données local. Pour savoir comment configurer ces ressources dans une requête, consultez [Utiliser des requêtes delta pour suivre les modifications apportées aux données de Microsoft Graph](/graph/delta-query-overview).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---august-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD – Août 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** Intégration tierce

En août 2020, nous avons ajouté les 25 applications suivantes à notre galerie d’applications avec prise en charge de la fédération :

[Backup365](https://portal.backup365.io/login), [Soapbox](https://app.soapboxhq.com/create?step=auth&provider=azure-ad2-oauth2), [Alma SIS](https://almau.getalma.com/), [Enlyft Dynamics 365 Connector](http://enlyft.com/), [Serraview Space Utilization Software Solutions](../saas-apps/serraview-space-utilization-software-solutions-tutorial.md), [Uniq](https://web.uniq.app/), [Visibly](../saas-apps/visibly-tutorial.md), [Zylo](../saas-apps/zylo-tutorial.md), [Edmentum - Courseware Assessments Exact Path](https://auth.edmentum.com/elf/login), [CyberLAB](https://cyberlab.evolvesecurity.com/#/welcome), [Altamira HRM](../saas-apps/altamira-hrm-tutorial.md), [WireWheel](../saas-apps/wirewheel-tutorial.md), [Zix Compliance and Capture](https://sminstall.zixcorp.com/teams/teams.php?install_request=true&tenant_id=common), [Greenlight Enterprise Business Controls Platform](../saas-apps/greenlight-enterprise-business-controls-platform-tutorial.md), [Genetec Clearance](https://www.clearance.network/), [iSAMS](../saas-apps/isams-tutorial.md), [VeraSMART](../saas-apps/verasmart-tutorial.md), [Amiko](https://amiko.web.rivero.app/), [Twingate](https://auth.twingate.com/signup), [Funnel Leasing](https://nestiolistings.com/sso/oidc/azure/authorize/), [Scalefusion](https://scalefusion.com/users/sign_in/), [Bpanda](https://goto.bpanda.com/login), [Vivun Calendar Connect](https://app.vivun.com/dashboard/calendar/connect), [FortiGate SSL VPN](../saas-apps/fortigate-ssl-vpn-tutorial.md), [Wandera End User](https://www.wandera.com/)

La documentation de toutes ces applications est disponible ici https://aka.ms/AppsTutorial

Pour référencer votre application dans la galerie d’applications Azure AD, lisez les informations détaillées ici : https://aka.ms/AzureADAppRequest

---

### <a name="resource-forests-now-available-for-azure-ad-ds"></a>Les forêts de ressources sont désormais disponibles pour Azure AD DS 

**Type :** Nouvelle fonctionnalité **Catégorie de service :** Services de domaine Azure AD   
**Fonctionnalité de produit :** Services de domaine Azure AD
 
La capacité des forêts de ressources dans Azure AD Domain Services est désormais généralement disponible. Vous pouvez désormais activer l’autorisation sans synchronisation de hachage de mot de passe pour utiliser Azure AD Domain Services, notamment l’autorisation par carte à puce. Pour en savoir plus, consultez [Concepts et fonctionnalités des jeux de réplicas pour Azure Active Directory Domain Services (préversion)](../../active-directory-domain-services/concepts-replica-sets.md).
 
---

### <a name="regional-replica-support-for-azure-ad-ds-managed-domains-now-available"></a>Prise en charge des réplicas régionaux pour les domaines gérés par Azure AD DS désormais disponible

**Type :** Nouvelle fonctionnalité   
**Catégorie de service :** Services de domaine Azure AD  
**Fonctionnalité de produit :** Services de domaine Azure AD
 
Vous pouvez étendre un domaine managé pour avoir plusieurs jeux de réplicas par locataire Azure AD. Les jeux de réplicas peuvent être ajoutés à n’importe quel réseau virtuel appairé dans toute région Azure prenant en charge Azure Active Directory Domain Services. D’autres jeux de réplicas dans des régions Azure différentes assurent la récupération d’urgence géographique pour les applications héritées si une région Azure est mise hors connexion. Pour en savoir plus, consultez [Concepts et fonctionnalités des jeux de réplicas pour Azure Active Directory Domain Services (préversion)](../../active-directory-domain-services/concepts-replica-sets.md).

---

### <a name="general-availability-of-azure-ad-my-sign-ins"></a>Disponibilité générale de Mes connexions Azure AD

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Expériences d’utilisateur final
 
La nouvelle fonctionnalité Mes connexions Azure AD permet aux utilisateurs d’entreprise d’examiner leur historique de connexion pour vérifier l’absence de toute activité inhabituelle. Elle permet en outre aux utilisateurs finaux de signaler s’ils étaient ou non à l’origine d’activités suspectes. Pour en savoir plus sur l’utilisation de cette fonctionnalité, consultez [Afficher et rechercher votre activité de connexion récente à partir de la page Mes connexions](../user-help/my-account-portal-sign-ins-page.md#confirm-unusual-activity).
 
---

### <a name="sap-successfactors-hr-driven-user-provisioning-to-azure-ad-is-now-generally-available"></a>L’approvisionnement piloté par SAP SuccessFactors RH d’utilisateurs vers Azure AD est désormais généralement disponible

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Vous pouvez à présent intégrer SAP SuccessFactors en tant que source d’identité faisant autorité avec Azure AD, et automatiser le cycle de vie de bout en bout des identités à l’aide d’événements de RH tels que de nouvelles embauches et des démissions pour conduire l’approvisionnement et le désapprovisionnement de comptes dans Azure AD. 

Pour en savoir plus sur la configuration de l’approvisionnement entrant de SAP SuccessFactors vers Azure AD, consultez le didacticiel [Configurer l’approvisionnement d’utilisateurs SAP SuccessFactors vers Active Directory](../saas-apps/sap-successfactors-inbound-provisioning-tutorial.md).
 
---

### <a name="custom-open-id-connect-ms-graph-api-support-for-azure-ad-b2c"></a>Prise en charge personnalisée de l’API MS Graph Open ID Connect pour Azure AD B2C

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2C - Gestion des identités consommateurs  
**Fonctionnalité de produit :** B2B/B2C
 
Auparavant, des fournisseurs d’Open ID Connect personnalisés ne pouvaient être ajoutés ou gérés que via le portail Azure. Les clients Azure AD B2C peuvent désormais ajouter et gérer ces fournisseurs également via la version bêta des API Microsoft Graph. Pour savoir comment configurer cette ressource à l’aide d’API, consultez [type de ressource identityProvider](/graph/api/resources/identityprovider?view=graph-rest-beta).
 
---

### <a name="assign-azure-ad-built-in-roles-to-cloud-groups"></a>Affecter des rôles intégrés Azure AD à des groupes cloud

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Rôles Azure AD  
**Fonctionnalité de produit :** Contrôle d’accès

Vous pouvez désormais attribuer des rôles intégrés Azure AD à des groupes cloud avec cette nouvelle fonctionnalité. Par exemple, vous pouvez attribuer le rôle Administrateur SharePoint au groupe Contoso_SharePoint_Admins. Vous pouvez également utiliser PIM pour faire du groupe un membre éligible du rôle, au lieu d’accorder un accès permanent. Pour découvrir comment configurer cette fonctionnalité, consultez [Utiliser des groupes cloud pour gérer les attributions de rôles dans Azure Active Directory (préversion)](../roles/groups-concept.md).
 
---

### <a name="insights-business-leader-built-in-role-now-available"></a>Rôle intégré Leader d’entreprise Insights désormais disponible

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Rôles Azure AD  
**Fonctionnalité de produit :** Contrôle d’accès
 
Les utilisateurs titulaires du rôle Leader d’entreprise Insights peuvent accéder à un ensemble de tableaux de bord et d’insights via l’[application M365 Insights](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics). Ceci inclut l’accès total à tous les tableaux de bord et aux insights présentés et la fonctionnalité d’exploration de données. Les utilisateurs titulaires de ce rôle n’ont pas accès aux paramètres de configuration du produit. Cette responsabilité est dévolue au rôle Administrateur Insights. Pour en savoir plus, consultez [Autorisations des rôles d’administrateur dans Azure Active Directory](../roles/permissions-reference.md#insights-business-leader).
 
---

### <a name="insights-administrator-built-in-role-now-available"></a>Rôle intégré Administrateur Insights désormais disponible

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Rôles Azure AD  
**Fonctionnalité de produit :** Contrôle d’accès
 
Les utilisateurs titulaires du rôle Insights Administrator peuvent accéder à l’ensemble des fonctionnalités d’administration de l’[application M365 Insights](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics). Un utilisateur titulaire de rôle peut lire les informations d’annuaire, surveiller l’intégrité du service, soumettre des tickets de support et accéder aux paramètres d’Administrateur Insights. Pour en savoir plus, consultez [Autorisations des rôles d’administrateur dans Azure Active Directory](../roles/permissions-reference.md#insights-administrator).
 
--- 

### <a name="application-admin-and-cloud-application-admin-can-manage-extension-properties-of-applications"></a>Un Administrateur d’application ou un Administrateur d’application cloud peuvent gérer les propriétés d’extension des applications

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Rôles Azure AD  
**Fonctionnalité de produit :** Contrôle d’accès
 
Auparavant, seul l’Administrateur général pouvait gérer la [propriété d’extension](/graph/api/application-post-extensionproperty?view=graph-rest-beta&tabs=http). Nous allons désormais activer cette fonctionnalité pour l’Administrateur d’application et l’Administrateur d’application cloud.
 
---

### <a name="mim-2016-sp2-hotfix-462630-and-connectors-1113010"></a>Correctif logiciel MIM 2016 SP2 4.6.263.0 et connecteurs 1.1.1301.0

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Microsoft Identity Manager  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités

Un [correctif cumulatif (build 4.6.263.0)](https://support.microsoft.com/help/4576473/hotfix-rollup-package-build-4-6-263-0-is-available-for-microsoft-ident) est disponible pour Microsoft Identity Manager (MIM) 2016 Service Pack 2 (SP2). Ce package cumulatif contient des mises à jour pour les composants MIM CM, Gestionnaire de synchronisation MIM et PAM. En outre, la build de connecteurs génériques MIM 1.1.1301.0 inclut des mises à jour du connecteur Graph.

---
 
## <a name="july-2020"></a>Juillet 2020

### <a name="as-an-it-admin-i-want-to-target-client-apps-using-conditional-access"></a>En tant qu’administrateur informatique, je souhaite cibler des applications clientes à l’aide de l’accès conditionnel

**Type :** Modification planifiée   
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
Avec la version en disponibilité générale de la condition des applications clientes dans l’accès conditionnel, les nouvelles stratégies s’appliquent désormais par défaut à toutes les applications clientes. Cela inclut les clients d’authentification hérités. Les stratégies existantes resteront inchangées, mais le bouton *ConfigurerOui/Non* sera supprimé des stratégies existantes pour identifier facilement les applications clientes qui sont appliquées par la stratégie. 

Lorsque vous créez une nouvelle stratégie, veillez à exclure les utilisateurs et les comptes de service qui utilisent encore l’authentification héritée. Si ce n’est pas le cas, ils seront bloqués. [Plus d’informations](../conditional-access/concept-conditional-access-conditions.md)
 
---

### <a name="upcoming-scim-compliance-fixes"></a>Prochains correctifs de conformité SCIM

**Type :** Modification planifiée  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Le service de provisionnement Azure AD utilise la norme SCIM pour l’intégration avec les applications. Notre implémentation de la norme SCIM est en cours d’évolution et nous nous attendons à apporter des modifications à notre comportement sur la façon dont nous effectuons les opérations PATCH, ainsi que la définition de la propriété « active » sur une ressource. [Plus d’informations](../app-provisioning/application-provisioning-config-problem-scim-compatibility.md)
 
---

### <a name="group-owner-setting-on-azure-admin-portal-will-be-changed"></a>Le paramètre propriétaire du groupe sur le portail d’administration Azure sera modifié

**Type :** Modification planifiée  
**Catégorie de service :** Gestion des groupes  
**Fonctionnalité de produit :** Collaboration

Les paramètres de propriétaire sur la page des paramètres généraux des groupes peuvent être configurés pour restreindre les privilèges d’attribution de propriétaire à un groupe limité d’utilisateurs dans le portail d’administration Azure et le panneau d’accès. Nous aurons bientôt la possibilité d’affecter des privilèges de propriétaire de groupe non seulement sur ces deux portails d’expérience utilisateur, mais également d’appliquer la stratégie sur le serveur principal pour fournir un comportement cohérent entre les points de terminaison, tels que PowerShell et Microsoft Graph. 

Nous allons commencer à désactiver le paramètre actuel pour les clients qui ne l’utilisent pas et offriront une option d’étendue aux utilisateurs pour le privilège de propriétaire de groupe dans les prochains mois. Pour obtenir des conseils sur la mise à jour des paramètres de groupe, consultez modifier les informations de votre groupe à l’aide d’[Azure Active Directory](./active-directory-groups-settings-azure-portal.md?context=azure%2factive-directory%2fusers-groups-roles%2fcontext%2fugr-context).

---

### <a name="azure-active-directory-registration-service-is-ending-support-for-tls-10-and-11"></a>Le service d’inscription Azure Active Directory met fin à la prise en charge de TLS 1.0 et 1.1

**Type :** Modification planifiée  
**Catégorie de service :** Gestion et inscription des appareils  
**Fonctionnalité de produit :** plateforme

Transport Layer Security (TLS) 1.2 et les serveurs et clients de mise à jour communiqueront bientôt avec Azure Active Directory Device Registration service. Le support de TLS 1.0 et 1.1 pour la communication avec Azure AD Device Registration service sera retiré :
- Le 31 août 2020, dans tous les clouds souverains (GCC High, DoD, etc.)
- Le 30 octobre 2020, dans tous les clouds commerciaux

[En savoir plus](../devices/reference-device-registration-tls-1-2.md) sur le protocole TLS 1.2 pour Azure AD Registration Service.

---

### <a name="windows-hello-for-business-sign-ins-visible-in-azure-ad-sign-in-logs"></a>Connexions Windows Hello entreprise visibles dans les journaux de connexion Azure AD

**Type :** Résolution  
**Catégorie de service :** Signalement  
**Fonctionnalité de produit :** Monitoring et création de rapports
 
Windows Hello Entreprise permet aux utilisateurs finaux de se connecter à des ordinateurs Windows en un geste (par exemple, un code confidentiel ou une biométrie). Les administrateurs Azure AD peuvent souhaiter différencier les connexions Windows Hello Entreprise des autres connexions Windows dans le cadre de l’authentification sans mot de passe d’une organisation. 

Les administrateurs peuvent maintenant voir si une authentification Windows a utilisé Windows Hello Entreprise en consultant l’onglet Détails de l’authentification pour un événement de connexion Windows dans le volet Connexions Azure AD dans le portail Azure. Les authentifications Windows Hello Entreprise incluront « WindowsHelloForBusiness » dans le champ méthode d’authentification. Pour plus d’informations sur l’interprétation des journaux de connexion, reportez-vous à la [Documentation des journaux de connexion](../reports-monitoring/concept-sign-ins.md).
 
---

### <a name="fixes-to-group-deletion-behavior-and-performance-improvements"></a>Résolutions pour le comportement de suppression des groupes et améliorations des performances

**Type :** Résolution  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Auparavant, lorsqu'un groupe passait de « in-scope » à « out of scope » et qu'un administrateur cliquait sur « restart » avant que la modification ne soit terminée, l'objet du groupe n'était pas supprimé. À présent, l’objet de groupe sera supprimé de l’application cible lorsqu’il sort de l’étendue (désactivé, supprimé, non assigné ou échec du filtre d’étendue). [Plus d’informations](../app-provisioning/how-provisioning-works.md#incremental-cycles)
 
---

### <a name="public-preview-admins-can-now-add-custom-content-in-the-email-to-reviewers-when-creating-an-access-review"></a>Préversion publique : Les administrateurs peuvent désormais ajouter du contenu personnalisé à l’e-mail aux réviseurs lors de la création d’une révision d’accès

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Révisions d’accès  
**Fonctionnalité de produit :** Gouvernance des identités
 
Lorsqu’une nouvelle révision d’accès est créée, le réviseur reçoit un e-mail lui demandant d’effectuer la révision d’accès. La plupart de nos clients ont demandé la possibilité d’ajouter du contenu personnalisé à l’e-mail, comme des informations de contact, ou d’autres contenus de support supplémentaires pour guider le réviseur. 

Désormais disponible en préversion publique, les administrateurs peuvent spécifier du contenu personnalisé dans l’e-mail envoyé aux réviseurs en ajoutant du contenu dans la section « avancé » des révisions d’accès Azure AD. Pour des conseils sur la création d’une révision d’accès des groupes, consultez [Créer une révision d’accès des groupes et applications dans les révisions d’accès Azure AD](../governance/create-access-review.md).
 
---

### <a name="authorization-code-flow-for-single-page-apps-available"></a>Flux du code d’autorisation pour les applications à page unique disponible

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Expérience de développement
 
Du fait des restrictions sur les cookies tiers dans les navigateurs modernes, telles que ITP de Safari, les application à page unique (SPA) doivent utiliser le flux du code d’autorisation, plutôt que le flux implicite, pour maintenir l’authentification unique. MSAL.js v 2.x prend désormais en charge le flux du code d’autorisation. 

Des mises à jour correspondantes étant présentes sur le portail Azure, vous pouvez actualiser votre SPA pour qu’il soit de type « spa » et utilise le flux du code d’authentification. Pour plus de conseils, consultez [Connecter des utilisateurs et obtenir un jeton d’accès dans une application à page unique JavaScript à l’aide du flux de code d’authentification](../develop/quickstart-v2-javascript-auth-code.md).
 
---

### <a name="azure-ad-application-proxy-now-supports-the-remote-desktop-services-web-client"></a>Le Proxy d’application Azure AD prend désormais en charge le Client Web Services Bureau à distance

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Proxy d’application  
**Fonctionnalité de produit :** Contrôle d’accès

Le Proxy d’application Azure AD prend désormais en charge le Client Web Services Bureau à distance (RDS). Le client web RDS permet aux utilisateurs d'accéder à l'infrastructure Bureau distant via tout navigateur compatible HTLM5 tel que Microsoft Edge, Internet Explorer 11, Google Chrome, etc. Les utilisateurs peuvent interagir avec des applications ou des bureaux distants, comme ils le feraient avec un appareil local depuis n’importe où. En utilisant le Proxy d’application Azure AD, vous pouvez augmenter la sécurité de votre déploiement des services Bureau à distance en appliquant la pré-authentification et les stratégies d’accès conditionnel pour tous les types d’applications clientes riches. Pour plus d’informations, consultez [Publier le Bureau à distance avec le Proxy d’application d’Azure AD](../manage-apps/application-proxy-integrate-with-remote-desktop-services.md).
 
---

### <a name="next-generation-azure-ad-b2c-user-flows-in-public-preview"></a>Flux utilisateur Azure AD B2C de nouvelle génération en préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2C - Gestion des identités consommateurs  
**Fonctionnalité de produit :** B2B/B2C
 
L'expérience de flux d'utilisateurs simplifiée offre la parité des fonctions avec les fonctions d'aperçu et est le foyer de toutes les nouvelles fonctionnalités. Les utilisateurs pourront activer de nouvelles fonctionnalités au sein du même flux d'utilisateurs, ce qui réduira la nécessité de créer plusieurs versions à chaque nouvelle sortie de fonctionnalité. Enfin, la nouvelle expérience utilisateur conviviale simplifie la sélection et la création de flux utilisateur. Essayez-la dès maintenant en [créant flux d’utilisateur](../../active-directory-b2c/tutorial-create-user-flows.md). 

Pour plus d'informations sur les flux d'utilisateurs, voir [Versions des flux d'utilisateurs dans Azure Active Directory B2C](../../active-directory-b2c/user-flow-versions.md#:~:text=    User flow  ,account. Usi ...  1 more rows ).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---july-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD - Juillet 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** Intégration tierce
 
En juillet 2020, nous avons ajouté les 55 applications suivantes à notre galerie d’applications avec prise en charge de la fédération :

[Clap Your Hands](http://www.rmit.com.ar/), [Appreiz](https://microsoftteams.appreiz.com/), [Inextor Vault](https://inexto.com/inexto-suite/inextor), [Beekast](https://my.beekast.com/), [Templafy OpenID Connect](https://app.templafy.com/), [PeterConnects receptionist](https://msteams.peterconnects.com/), [AlohaCloud](https://appfusions.alohacloud.com/auth), [Control Tower](https://bpm.tnxcorp.com/sso/microsoft), [Cocoom](https://start.cocoom.com/), [COINS Construction Cloud](https://sso.coinsconstructioncloud.com/#login/), [Medxnote MT](https://task.teamsmain.medx.im/authorization), [Reflekt](https://reflekt.konsolute.com/login), [Rever](https://app.reverscore.net/access), [MyCompanyArchive](https://login.mycompanyarchive.com/), [GReminders](https://app.greminders.com/o365-oauth), [Titanfile](../saas-apps/titanfile-tutorial.md), [Wootric](../saas-apps/wootric-tutorial.md), [SolarWinds Orion](https://support.solarwinds.com/SuccessCenter/s/orion-platform?language=en_US),  [OpenText Directory Services](../saas-apps/opentext-directory-services-tutorial.md), [Datasite](../saas-apps/datasite-tutorial.md), [BlogIn](../saas-apps/blogin-tutorial.md), [IntSights](../saas-apps/intsights-tutorial.md), [kpifire](../saas-apps/kpifire-tutorial.md), [Textline](../saas-apps/textline-tutorial.md), [Cloud Academy - SSO](../saas-apps/cloud-academy-sso-tutorial.md), [Community Spark](../saas-apps/community-spark-tutorial.md), [Chatwork](../saas-apps/chatwork-tutorial.md), [CloudSign](../saas-apps/cloudsign-tutorial.md), [C3M Cloud Control](../saas-apps/c3m-cloud-control-tutorial.md), [SmartHR](https://smarthr.jp/), [NumlyEngage™](../saas-apps/numlyengage-tutorial.md), [Michigan Data Hub Single Sign-On](../saas-apps/michigan-data-hub-single-sign-on-tutorial.md), [Egress](../saas-apps/egress-tutorial.md), [SendSafely](../saas-apps/sendsafely-tutorial.md), [Eletive](https://app.eletive.com/), [Right-Hand Cybersecurity ADI](https://right-hand.ai/), [Fyde Enterprise Authentication](https://enterprise.fyde.com/), [Verme](../saas-apps/verme-tutorial.md), [Lenses.io](../saas-apps/lensesio-tutorial.md), [Momenta](../saas-apps/momenta-tutorial.md), [Uprise](https://app.uprise.co/sign-in), [Q](https://q.moduleq.com/login), [CloudCords](../saas-apps/cloudcords-tutorial.md), [TellMe Bot](https://tellme365liteweb.azurewebsites.net/), [Inspire](https://app.inspiresoftware.com/), [Maverics Identity Orchestrator SAML Connector](https://www.strata.io/identity-fabric/), [Smartschool (School Management System)](https://smartschoolz.com/login), [Zepto - Intelligent timekeeping](https://user.zepto-ai.com/signin), [Studi.ly](https://studi.ly/), [Trackplan](http://www.trackplanfm.com/), [Skedda](../saas-apps/skedda-tutorial.md), [WhosOnLocation](../saas-apps/whos-on-location-tutorial.md), [Coggle](../saas-apps/coggle-tutorial.md), [Kemp LoadMaster](https://kemptechnologies.com/cloud-load-balancer/), [BrowserStack Single Sign-on](../saas-apps/browserstack-single-sign-on-tutorial.md)

La documentation de toutes ces applications est disponible ici https://aka.ms/AppsTutorial

Pour lister votre application dans la galerie d’applications Azure AD, veuillez lire les informations détaillées ici : https://aka.ms/AzureADAppRequest

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---july-2020"></a>Nouveaux connecteurs de provisionnement dans la galerie d’applications Azure AD - Juillet 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Intégration tierce

Vous pouvez désormais automatiser la création, la mise à jour et la suppression de comptes d’utilisateur pour la nouvelle application nouvellement intégrée [LinkedIn Learning](../saas-apps/linkedin-learning-provisioning-tutorial.md).

Pour découvrir comment sécuriser plus efficacement votre organisation à l’aide de l’approvisionnement automatique de comptes utilisateur, voir [Automatisation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure AD](../app-provisioning/user-provisioning.md).

---

### <a name="view-role-assignments-across-all-scopes-and-ability-to-download-them-to-a-csv-file"></a>Afficher les attributions de rôle dans toutes les étendues et la possibilité de les télécharger dans un fichier CSV

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Rôles Azure AD  
**Fonctionnalité de produit :** Contrôle d’accès
 
Vous pouvez maintenant afficher les attributions de rôle sur toutes les étendues d’un rôle sous l’onglet « Rôles et administrateurs » dans le portail Azure AD. Vous pouvez également télécharger ces attributions de rôle pour chaque rôle dans un fichier CSV. Pour obtenir des conseils sur l’affichage et l’ajout d’attributions de rôles, consultez [Afficher et affecter des rôles d’administrateur dans Azure Active Directory](../roles/manage-roles-portal.md).
 
---

### <a name="azure-multi-factor-authentication-software-development-azure-mfa-sdk-deprecation"></a>Désapprobation du développement de logiciels Azure Multi-Factor Authentication (kit de développement logiciel (SDK) Azure MFA)

**Type :** Déprécié  
**Catégorie de service :** MFA  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
Le développement de logiciels Azure Multi-Factor Authentication (kit de développement logiciel (SDK) Azure MFA) a atteint sa fin de vie le 14 novembre 2018, comme annoncé pour la première fois en novembre 2017. Microsoft va arrêter le service SDK en vigueur le 30 septembre 2020. Les appels passés au kit de développement logiciel (SDK) échouent.

Si votre organisation utilise le kit de développement logiciel (SDK) Azure MFA, vous devez migrer le 30 septembre 2020 :
- Kit de développement logiciel (SDK) Azure MFA pour MIM :  Si vous utilisez le kit de développement logiciel (SDK) avec MIM, vous devez migrer vers le serveur Azure MFA et activer Privileged Access Management (PAM) à la suite de ces [instructions](/microsoft-identity-manager/working-with-mfaserver-for-mim).   
- Kit de développement logiciel (SDK) Azure MFA pour les applications personnalisées : Envisagez d’intégrer votre application dans Azure AD et d’utiliser l’accès conditionnel pour appliquer l’authentification multifacteur. Pour commencer, consultez cette [page](../manage-apps/plan-an-application-integration.md). 

---

## <a name="june-2020"></a>Juin 2020 

### <a name="user-risk-condition-in-conditional-access-policy"></a>Condition de risque d’utilisateur dans la stratégie d’accès conditionnel

**Type :** Modification planifiée  
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités
 

La prise en charge des risques d’utilisateur dans une stratégie d’accès conditionnel Azure AD vous permet de créer plusieurs stratégies basées sur les risques de l’utilisateur. Différents niveaux de risque d’utilisateur minimum peuvent être nécessaires pour différents utilisateurs et applications. En fonction du risque de l’utilisateur, vous pouvez créer des stratégies pour bloquer l’accès, exiger une authentification multifacteur, la modification sécurisée du mot de passe ou une redirection vers Microsoft Cloud App Security pour appliquer une stratégie de session, par exemple un audit supplémentaire.

La condition de risque d’utilisateur requiert Azure AD Premium P2 car elle utilise Azure Identity Protection, qui est une offre P2. Pour plus d’informations sur l’accès conditionnel, consultez [Documentation relative à l’Accès conditionnel Azure Active Directory](../conditional-access/index.yml).

---

### <a name="saml-sso-now-supports-apps-that-require-spnamequalifier-to-be-set-when-requested"></a>L’authentification unique SAML prend désormais en charge les applications qui requièrent la définition de SPNameQualifier à la demande

**Type :** Résolution  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** SSO
 
Certaines applications SAML requièrent que SPNameQualifier soit retourné à la demande dans le sujet de l’assertion. Azure AD répond maintenant correctement lorsqu’un SPNameQualifier est demandé dans la stratégie NameID de la demande. Cette règle s’applique également à la connexion initiée par le fournisseur de service, et prochainement à la connexion initiée par le fournisseur d'identité.  Pour en savoir plus sur le protocole SAML dans Azure Active Directory, consultez [Protocole SAML d’authentification unique](../develop/single-sign-on-saml-protocol.md).

---

### <a name="azure-ad-b2b-collaboration-supports-inviting-msa-and-google-users-in-azure-government-tenants"></a>Azure AD B2B collaboration prend en charge l’invitation des utilisateurs MSA et Google dans les locataires Azure Government

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2B  
**Fonctionnalité de produit :** B2B/B2C
 

Les locataires Azure Government qui utilisent les fonctionnalités de collaboration B2B peuvent désormais inviter des utilisateurs disposant d’un compte Microsoft ou Google. Pour déterminer si votre locataire peut utiliser ces fonctionnalités, suivez les instructions fournies dans [Comment savoir si B2B Collaboration est disponible dans mon locataire Azure US Government ?](../external-identities/current-limitations.md#how-can-i-tell-if-b2b-collaboration-is-available-in-my-azure-us-government-tenant)

 
---
 
### <a name="user-object-in-ms-graph-v1-now-includes-externaluserstate-and-externaluserstatechangeddatetime-properties"></a>L’objet utilisateur dans MS Graph v1 comprend maintenant les propriétés externalUserState et externalUserStateChangedDateTime

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2B  
**Fonctionnalité de produit :** B2B/B2C
 

Les propriétés externalUserState et externalUserStateChangedDateTime peuvent être utilisées pour rechercher les invités B2B qui n’ont pas encore accepté leurs invitations, ainsi que l’automatisation des builds, notamment la suppression d’utilisateurs qui n’ont pas accepté leurs invitations après un certain nombre de jours. Ces propriétés sont désormais disponibles dans MS Graph v1. Pour obtenir des conseils sur l’utilisation de ces propriétés, reportez-vous à [Type de ressource utilisateur](/graph/api/resources/user?view=graph-rest-1.0).
 
---

### <a name="manage-authentication-sessions-in-azure-ad-conditional-access-is-now-generally-available"></a>La gestion des sessions d’authentification dans l’accès conditionnel Azure AD est désormais mise à la disposition générale

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
Les fonctionnalités de gestion des sessions d’authentification vous permettent de configurer la fréquence à laquelle vos utilisateurs doivent fournir des informations d’identification de connexion ainsi que des informations d’identification après la fermeture et la réouverture des navigateurs, pour offrir plus de sécurité et de flexibilité à votre environnement.
 
Par ailleurs, la gestion des sessions d’authentification ne s'appliquait auparavant qu'à l'authentification à un facteur sur les appareils joints à Azure AD, joints à Azure AD Hybride et inscrits auprès d’Azure AD. Désormais, la gestion des sessions d’authentification s’applique également à MFA. Pour plus d’informations, consultez [Configurer la gestion de session d’authentification avec l’accès conditionnel](../conditional-access/howto-conditional-access-session-lifetime.md).

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---june-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD - Juin 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** Intégration tierce
 
En juin 2020, nous avons ajouté les 29 nouvelles applications suivantes à notre galerie d’applications avec prise en charge de la fédération :

[Shopify Plus](../saas-apps/shopify-plus-tutorial.md), [Ekarda](../saas-apps/ekarda-tutorial.md), [MailGates](../saas-apps/mailgates-tutorial.md), [BullseyeTDP](../saas-apps/bullseyetdp-tutorial.md), [Raketa](../saas-apps/raketa-tutorial.md), [Segment](../saas-apps/segment-tutorial.md), [Ai Auditor](https://www.mindbridge.ai/products/ai-auditor/), [Pobuca Connect](https://app.pobu.ca/), [Proto.io](../saas-apps/proto.io-tutorial.md), [Gatekeeper](https://www.gatekeeperhq.com/), [Hub Planner](../saas-apps/hub-planner-tutorial.md), [Ansira-Partner Go-to-Market Toolbox](https://ansira.com/technology/channel-engagement), [IBM Digital Business Automation on Cloud](../saas-apps/ibm-digital-business-automation-on-cloud-tutorial.md), [Kisi Physical Security](../saas-apps/kisi-physical-security-tutorial.md), [ViewpointOne](https://team.viewpoint.com/), [IntelligenceBank](../saas-apps/intelligencebank-tutorial.md), [pymetrics](../saas-apps/pymetrics-tutorial.md), [Zero](https://www.teamzero.com/), [InStation](https://instation.invillia.com/), [edX for Business SAML 2.0 Integration](../saas-apps/edx-for-business-saml-integration-tutorial.md), [MOOC Office 365](https://mooc.office365-training.com/en/), [SmartKargo](../saas-apps/smartkargo-tutorial.md), [PKIsigning platform](https://platform.pkisigning.nl/), [SiteIntel](../saas-apps/siteintel-tutorial.md), [Field iD](../saas-apps/field-id-tutorial.md), [Curricula SAML](../saas-apps/curricula-saml-tutorial.md), [Perforce Helix Core - Helix Authentication Service](../saas-apps/perforce-helix-core-tutorial.md), [MyCompliance Cloud](https://cloud.metacompliance.com/), [Smallstep SSH](https://smallstep.com/sso-ssh/)  

La documentation de toutes ces applications est disponible ici https://aka.ms/AppsTutorial. Pour lister votre application dans la galerie d’applications Azure AD, veuillez lire les informations détaillées ici : https://aka.ms/AzureADAppRequest.

---

### <a name="api-connectors-for-external-identities-self-service-sign-up-are-now-in-public-preview"></a>Les connecteurs d’API pour l’inscription en libre-service des identités externes sont désormais en préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2B  
**Fonctionnalité de produit :** B2B/B2C
 
Les connecteurs d’API d’identités externes vous permettent de tirer parti des API Web pour intégrer l’inscription en libre-service à des systèmes cloud externes. Cela signifie que vous pouvez désormais appeler des API Web en tant qu’étapes spécifiques dans un flux d’inscription pour déclencher des flux de travail personnalisés basés sur le cloud. Par exemple, vous pouvez utiliser des connecteurs d’API pour :

- Intégrer à des flux de travaux d’approbation personnalisés.
- Effectuer une vérification d’identité
- Valider des données d’entrée utilisateur
- Remplacer des attributs utilisateur
- Exécuter une logique métier personnalisée

Pour plus d’informations sur toutes les expériences possibles avec les connecteurs d’API, consultez [Utiliser des connecteurs d’API pour personnaliser et étendre l’inscription en libre-service](../external-identities/api-connectors-overview.md) ou [Personnaliser l’inscription en libre-service d’identités externes avec des intégrations d’API Web](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/customize-external-identities-self-service-sign-up-with-web-api/ba-p/1257364#.XvNz2fImuQg.linkedin).
 
---

### <a name="provision-on-demand-and-get-users-into-your-apps-in-seconds"></a>Provisionner à la demande et faire accéder les utilisateurs à vos applications en quelques secondes

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Le service de provisionnement Azure AD fonctionne actuellement de façon cyclique. Le service s’exécute toutes les 40 minutes. La [fonctionnalité de provisionnement à la demande](https://aka.ms/provisionondemand) vous permet de choisir un utilisateur et de le configurer en quelques secondes. Cette fonctionnalité vous permet de résoudre rapidement les problèmes de provisionnement, sans avoir à relancer le cycle de provisionnement. 
 
---

### <a name="new-permission-for-using-azure-ad-entitlement-management-in-graph"></a>Nouvelle autorisation pour utiliser la gestion des droits d’utilisation Azure AD dans Graph

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Autres  
**Fonctionnalité de produit :** Gestion des droits d’utilisation
 
Une nouvelle autorisation déléguée EntitlementManagement.Read.All est désormais disponible pour une utilisation avec l’API de gestion des droits dans Microsoft Graph version bêta. Pour en savoir plus sur les API disponibles, consultez [Utilisation de l’API de gestion des droits Azure AD](/graph/api/resources/entitlementmanagement-root?view=graph-rest-beta).

---

### <a name="identity-protection-apis-available-in-v10"></a>API de protection des données disponibles dans la version 1.0

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Identity Protection  
**Fonctionnalité de produit :** Protection et sécurité des identités
 
Les API riskyUsers et riskDetections Microsoft Graph sont désormais mises à la disposition générale. Elles sont maintenant disponibles au niveau du point de terminaison v1.0, et nous vous invitons à les utiliser en production. Pour plus d’informations, consultez la [documentation Microsoft Graph](/graph/api/resources/identityprotectionroot?view=graph-rest-1.0).
 
---

### <a name="sensitivity-labels-to-apply-policies-to-microsoft-365-groups-is-now-generally-available"></a>Les étiquettes de sensibilité permettant d’appliquer des stratégies à des groupes Microsoft 365 sont désormais mises à la disposition générale

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Gestion des groupes  
**Fonctionnalité de produit :** Collaboration
 

Vous pouvez maintenant créer des étiquettes de sensibilité et utiliser les paramètres d’étiquette pour appliquer des stratégies à des groupes Microsoft 365, notamment la confidentialité (publique ou privée) et la stratégie d’accès utilisateur externe. Vous pouvez créer une étiquette avec la stratégie de confidentialité privée et une stratégie d’accès utilisateur externe pour ne pas autoriser l’ajout d’utilisateurs invités. Lorsqu’un utilisateur applique cette étiquette à un groupe, le groupe est privé et aucun utilisateur invité n’est autorisé à y être ajouté. 

Les étiquettes de sensibilité sont importantes pour protéger les données critiques de votre entreprise et vous permettre de gérer les groupes à grande échelle, de manière conforme et sécurisée. Pour obtenir des conseils sur l’utilisation des étiquettes de sensibilité, consultez [Attribuer des étiquettes de sensibilité aux groupes Microsoft 365 dans Azure Active Directory (préversion)](../enterprise-users/groups-assign-sensitivity-labels.md).
 
---

### <a name="updates-to-support-for-microsoft-identity-manager-for-azure-ad-premium-customers"></a>Mises à jour de la prise en charge de Microsoft Identity Manager pour les clients Azure AD Premium

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Microsoft Identity Manager  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
La prise en charge Azure est désormais disponible pour les composants d’intégration Azure AD de Microsoft Identity Manager 2016, jusqu’à la fin de la prise en charge étendue de Microsoft Identity Manager 2016. Pour en savoir plus, consultez [Mise à jour du support pour les clients Azure AD Premium utilisant Microsoft Identity Manager](/microsoft-identity-manager/support-update-for-azure-active-directory-premium-customers).

---

### <a name="the-use-of-group-membership-conditions-in-sso-claims-configuration-is-increased"></a>L’utilisation des conditions d’appartenance de groupe dans la configuration des revendications SSO a été augmentée

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** SSO
 
Auparavant, le nombre de groupes disponibles lors d’une modification conditionnelle des revendications en fonction de l’appartenance à un groupe dans une configuration d’application unique était limité à 10. L’utilisation des conditions d’appartenance de groupe dans la configuration des revendications SSO a maintenant été augmentée à un maximum de 50 groupes. Pour plus d’informations sur la configuration des revendications, reportez-vous à [Configuration des revendications SSO des applications d’entreprise](../develop/active-directory-saml-claims-customization.md#emitting-claims-based-on-conditions). 

---

### <a name="enabling-basic-formatting-on-the-sign-in-page-text-component-in-company-branding"></a>Activation de la mise en forme de base sur le composant Texte de la page de connexion dans la marque de société.

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Authentification utilisateur
 
La fonctionnalité Marque de société sur l’expérience de connexion Azure AD/Microsoft 365 a été mise à jour pour permettre au client d’ajouter des liens hypertexte et une mise en forme simple, y compris une police en gras, le soulignement et l’italique. Pour obtenir des conseils sur l’utilisation de cette fonctionnalité, voir [Personnaliser la page de connexion Azure Active Directory de votre organisation](./customize-branding.md).

---

### <a name="provisioning-performance-improvements"></a>Améliorations apportées aux performances de provisionnement

**Type :** Fonctionnalité modifiée  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Le service de provisionnement a été mis à jour pour réduire le temps nécessaire à l’exécution d’un [cycle incrémentiel](../app-provisioning/how-provisioning-works.md#incremental-cycles). Cela signifie que les utilisateurs et les groupes seront provisionnés dans leurs applications plus rapidement qu’auparavant. Toutes les tâches de provisionnement créées après le 10/06/2020 bénéficient automatiquement des améliorations de performances. Toutes les applications configurées pour un provisionnement avant le 10/06/2020 devront redémarrer une fois après cette date pour tirer parti des améliorations de performances. 

---

### <a name="announcing-the-deprecation-of-adal-and-ms-graph-parity"></a>Annonce de la dépréciation d’ADAL et de la parité MS Graph

**Type :** Déprécié  
**Catégorie de service :** N/A  
**Fonctionnalité de produit :** Gestion du cycle de vie des appareils

Maintenant que Microsoft Authentication Libraries (MSAL) est disponible, nous n’ajouterons plus de nouvelles fonctionnalités à Azure Active Directory Authentication Libraries (ADAL) et arrêterons les correctifs de sécurité le 30 juin 2022. Pour plus d’informations sur la migration vers MSAL, reportez-vous à [Migrer des applications vers la bibliothèque d’authentification Microsoft (MSAL)](../develop/msal-migration.md).

En outre, nous avons terminé la préparation de toutes les fonctionnalités Azure AD Graph disponibles via MS Graph. Ainsi, les API Graph Azure AD recevront uniquement des correctifs de bogues et de sécurité jusqu’au 30 juin 2022. Pour plus d’informations, consultez [Mettre à jour vos applications pour utiliser la bibliothèque d’authentification Microsoft et l’API Microsoft Graph](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363)
 
---
 
## <a name="may-2020"></a>Mai 2020

### <a name="retirement-of-properties-in-signins-riskyusers-and-riskdetections-apis"></a>Mise hors service des propriétés dans les API signIns, riskyUsers et riskDetections

**Type :** Modification planifiée  
**Catégorie de service :** Identity Protection  
**Fonctionnalité de produit :** Protection et sécurité des identités

Actuellement, les types énumérés sont utilisés pour représenter la propriété riskType à la fois dans l’API riskDetections et dans riskyUserHistoryItem (en préversion). Les types énumérés sont également utilisés pour la propriété riskEventTypes dans l’API signIns. À l’avenir, nous représenterons ces propriétés sous forme de chaînes. 

Les clients doivent effectuer la transition vers la propriété riskEventType dans la version bêta des API riskDetections et riskyUserHistoryItem, et pour la propriété riskEventTypes_v2 dans la version bêta de l’API signIns d’ici au 9 septembre 2020. À cette date, nous mettrons hors service les propriétés riskType et riskEventTypes actuelles. Pour plus d’informations, reportez-vous à [Modifications apportées aux propriétés d’événements à risque et aux API de protection d’identité sur Microsoft Graph](https://developer.microsoft.com/graph/blogs/changes-to-risk-event-properties-and-identity-protection-apis-on-microsoft-graph/).

--- 

### <a name="deprecation-of-riskeventtypes-property-in-signins-v10-api-on-microsoft-graph"></a>Dépréciation de la propriété riskEventTypes dans l’API signIns v1.0 sur Microsoft Graph

**Type :** Modification planifiée  
**Catégorie de service :** Signalement  
**Fonctionnalité de produit :** Protection et sécurité des identités

Les types énumérés basculeront vers les types chaîne s’ils représentent des propriétés d’événement à risque dans Microsoft Graph en septembre 2020. En plus de l’impact sur les API en préversion, cette modification affectera également l’API signIns en production.

Nous avons introduit une nouvelle propriété riskEventsTypes_v2 (chaîne) pour l’API signIns v1.0. Nous mettrons hors service la propriété riskEventTypes (enum) actuelle le 11 juin 2022, conformément à notre stratégie de dépréciation de Microsoft Graph. Les clients doivent passer à la propriété riskEventTypes_v2 dans l’API signIns v1.0 avant le 11 juin 2022. Pour plus d’informations, consultez [Dépréciation de la propriété riskEventTypes dans l’API signIns v1.0 sur Microsoft Graph](https://developer.microsoft.com/graph/blogs/deprecation-of-riskeventtypes-property-in-signins-v1-0-api-on-microsoft-graph//).

--- 

### <a name="upcoming-changes-to-mfa-email-notifications"></a>Modifications à venir concernant les notifications par e-mail MFA

**Type :** Modification planifiée  
**Catégorie de service :** MFA  
**Fonctionnalité de produit :** Protection et sécurité des identités
 

Nous apportons les modifications suivantes aux notifications par e-mail pour la MFA cloud :

Des notifications par e-mail vont être envoyées à partir de l’adresse suivante : azure-noreply@microsoft.com et msonlineservicesteam@microsoftonline.com. Nous mettons à jour le contenu des e-mails d’alerte de fraude afin de mieux indiquer les étapes à suivre pour débloquer les utilisations.

---

### <a name="new-self-service-sign-up-for-users-in-federated-domains-who-cant-access-microsoft-teams-because-they-arent-synced-to-azure-active-directory"></a>Nouvelle inscription en libre-service pour les utilisateurs des domaines fédérés qui ne peuvent pas accéder à Microsoft teams parce qu’ils ne sont pas synchronisés à Azure Active Directory.

**Type :** Modification planifiée  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Authentification utilisateur
 

Actuellement, les utilisateurs qui se trouvent sur des domaines fédérés dans Azure AD, mais qui ne sont pas synchronisés avec le locataire, ne peuvent pas accéder à Teams. À partir de la fin juin, cette nouvelle possibilité leur permettra de le faire par l’extension de la fonctionnalité d’inscription vérifiée par e-mail. Les utilisateurs qui peuvent se connecter à un fournisseur d’identité fédéré, mais qui ne possèdent pas encore d’objet utilisateur dans Azure ID, seront en mesure d’obtenir cet objet créé automatiquement, et d’être authentifié pour Teams. Leur objet utilisateur sera désigné en tant que « inscription en libre-service ». Il s’agit d’une extension de la capacité existante à effectuer une inscription automatique vérifiée par e-mail, à laquelle les utilisateurs des domaines gérés peuvent procéder et avec laquelle ils peuvent être contrôlés à l’aide du même indicateur. Cette modification s’effectuera lors du déploiement se déroulant dans les deux prochains mois. Retrouvez les mises à jour de la documentation [ici](../enterprise-users/directory-self-service-signup.md).
 
---

### <a name="upcoming-fix-the-oidc-discovery-document-for-the-azure-government-cloud-is-being-updated-to-reference-the-correct-graph-endpoints"></a>Correctif à venir : Le document de découverte OIDC pour le cloud Azure Government est mis à jour pour faire référence aux points de terminaison Graph appropriés.

**Type :** Modification planifiée  
**Catégorie de service :** Clouds souverains  
**Fonctionnalité de produit :** Authentification utilisateur
 
À partir de juin, le document de découverte OIDC, [Microsoft Identity Platform and OpenID Connect Protocol](../develop/v2-protocols-oidc.md) (Plateforme d’identités Microsoft et protocole OpenID Connect), relatif au point de terminaison [Cloud Azure Government](../develop/authentication-national-cloud.md) (login.microsoftonline.us), va commencer à retourner le point de terminaison [Graph du cloud national](/graph/deployments) approprié (https://graph.microsoft.us ou https://dod-graph.microsoft.us), en fonction du locataire fourni.  Il présente actuellement le champ « msgraph_host » incorrect du point de terminaison Graph (graph.microsoft.com).  

Ce correctif de bogue sera progressivement déployé sur une période de 2 mois environ.  

---

### <a name="azure-government-users-will-no-longer-be-able-to-sign-in-on-loginmicrosoftonlinecom"></a>Les utilisateurs d’Azure Government ne seront plus en mesure de se connecter à login.microsoftonline.com

**Type :** Planifier la modification  
**Catégorie de service :** Clouds souverains  
**Fonctionnalité de produit :** Authentification utilisateur
 
Le 1er juin 2018, l’adresse de l’autorité officielle Azure Active Directory (Azure AD) pour Azure Government a changé de https://login-us.microsoftonline.com en https://login.microsoftonline.us. Si vous possédez une application au sein d’un locataire Azure Government, vous devez mettre à jour votre application pour qu’elle connecte les utilisateurs sur le point de terminaison .us.

À partir du 5 mai, Azure AD commencera à appliquer le changement de point de terminaison en empêchant les utilisateurs d’Azure Government de se connecter à des applications hébergées dans des locataires Azure Government à l’aide du point de terminaison public (microsoftonline.com). Les applications impactées commenceront à afficher une erreur AADSTS900439-USGClientNotSupportedOnPublicEndpoint. 

Un déploiement progressif de cette modification va avoir lieu, dont la mise en application est prévue de s’achever sur l’ensemble des applications en juin 2020. Pour plus d’informations, consultez le [billet de blog Azure Government](https://devblogs.microsoft.com/azuregov/azure-government-aad-authority-endpoint-update/).

---

### <a name="saml-single-logout-request-now-sends-nameid-in-the-correct-format"></a>La requête SAML Single logout envoie désormais NameID au format correct

**Type :** Résolution  
**Catégorie de service :** Authentifications (connexions)  
**Fonctionnalité de produit :** Authentification utilisateur
 
Lorsqu’un utilisateur clique sur la déconnexion (par exemple, dans le portail MyApps), Azure AD envoie un message SAML Single Logout à chaque application qui est active dans la session utilisateur et pour laquelle une URL de déconnexion est configurée. Ces messages contiennent un NameID dans un format persistant.

Si le jeton de connexion SAML d’origine a utilisé un format différent pour NameID (par exemple, e-mail/UPN), l’application SAML ne peut pas mettre en corrélation le NameID du message de déconnexion avec une session existante (puisque les NameID utilisés dans les deux messages sont différents), ce qui a provoqué le rejet du message de déconnexion par l’application SAML, et le maintien de l’utilisateur connecté. Ce correctif met le message de déconnexion en adéquation avec le NameID configuré pour l’application.

---

### <a name="hybrid-identity-administrator-role-is-now-available-with-cloud-provisioning"></a>Le rôle d’administrateur d’identité hybride est désormais disponible avec le provisionnement cloud

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement cloud Azure AD  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Les administrateurs informatiques peuvent commencer à utiliser le nouveau rôle d’« administrateur hybride » en tant que rôle le moins privilégié pour configurer le provisionnement cloud Azure ADConnect. Avec ce nouveau rôle, vous n’avez plus besoin d’utiliser le rôle d’administrateur général pour installer et configurer le provisionnement cloud. [Plus d’informations](../roles/delegate-by-task.md#connect)
 
---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---may-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD - Mai 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** Intégration tierce
 
En mai 2020, nous avons ajouté les 36 applications suivantes à notre galerie d’applications avec prise en charge de la fédération :

[Moula](https://moula.com.au/pay/merchants), [Surveypal](https://www.surveypal.com/app), [Kbot365](https://www.konverso.ai/virtual-assistant-digital-workplace/), [TackleBox](http://www.tacklebox.app/), [Powell Teams](https://powell-software.com/en/powell-teams-en/), [Talentsoft Assistant](https://msteams.talent-soft.com/), [ASC Recording Insights](https://teams.asc-recording.app/product), [GO1](https://www.go1.com/), [B-Engaged](https://b-engaged.se/), [Competella Contact Center Workgroup](http://www.competella.com/), [Asite](http://www.asite.com/), [ImageSoft Identity](https://identity.imagesoftinc.com/), [My IBISWorld](https://identity.imagesoftinc.com/), [insuite](../saas-apps/insuite-tutorial.md), [Change Process Management](../saas-apps/change-process-management-tutorial.md), [Cyara CX Assurance Platform](../saas-apps/cyara-cx-assurance-platform-tutorial.md), [Smart Global Governance](../saas-apps/smart-global-governance-tutorial.md), [Prezi](../saas-apps/prezi-tutorial.md), [Mapbox](../saas-apps/mapbox-tutorial.md), [Datava Enterprise Service Platform](../saas-apps/datava-enterprise-service-platform-tutorial.md), [Whimsical](../saas-apps/whimsical-tutorial.md), [Trelica](../saas-apps/trelica-tutorial.md), [EasySSO for Confluence](../saas-apps/easysso-for-confluence-tutorial.md), [EasySSO for BitBucket](../saas-apps/easysso-for-bitbucket-tutorial.md), [EasySSO for Bamboo](../saas-apps/easysso-for-bamboo-tutorial.md), [Torii](../saas-apps/torii-tutorial.md), [Axiad Cloud](../saas-apps/axiad-cloud-tutorial.md), [Humanage](../saas-apps/humanage-tutorial.md), [ColorTokens ZTNA](../saas-apps/colortokens-ztna-tutorial.md), [CCH Tagetik](../saas-apps/cch-tagetik-tutorial.md), [ShareVault](../saas-apps/sharevault-tutorial.md), [Vyond](../saas-apps/vyond-tutorial.md), [TextExpander](../saas-apps/textexpander-tutorial.md), [Anyone Home CRM](../saas-apps/anyone-home-crm-tutorial.md), [askSpoke](../saas-apps/askspoke-tutorial.md), [ice Contact Center](../saas-apps/ice-contact-center-tutorial.md)

La documentation de toutes ces applications est disponible ici https://aka.ms/AppsTutorial.

Pour lister votre application dans la galerie d’applications Azure AD, veuillez lire les informations détaillées ici https://aka.ms/AzureADAppRequest.

---

### <a name="report-only-mode-for-conditional-access-is-now-generally-available"></a>Disponibilité générale du mode rapport seul pour l’accès conditionnel

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités

Le [mode rapport seul pour l’accès conditionnel Azure AD](../conditional-access/concept-conditional-access-report-only.md) vous permet d’évaluer le résultat d’une stratégie sans appliquer de contrôles d’accès. Vous pouvez tester les stratégies de rapport seul au sein de votre organisation afin de bien comprendre leur impact avant de les activer, ce qui rend leur déploiement à la fois plus sûr et plus facile. Ces derniers mois, nous avons constaté une adoption forte du mode rapport seul ; plus de 26 millions d’utilisateurs opèrent déjà dans le cadre d’une stratégie de rapport seul. Faisant suite à l’annonce d’aujourd’hui, les nouvelles stratégies d’accès conditionnel Azure AD seront créées par défaut en mode rapport seul. Cela signifie que vous pouvez surveiller l’impact de vos stratégies à partir du moment de leur création. Et ceux d’entre vous qui utilisent les API MS Graph peuvent également [gérer les stratégies de rapport seul par programmation](/graph/api/resources/conditionalaccesspolicy?view=graph-rest-beta). 

---

### <a name="self-service-sign-up-for-guest-users"></a>Inscription en libre-service pour les utilisateurs invités

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** B2B  
**Fonctionnalité de produit :** B2B/B2C
 
Avec les identités externes dans Azure AD, vous pouvez autoriser des personnes extérieures à votre organisation à accéder à vos applications et ressources tout en leur permettant de se connecter à l’aide de l’identité de leur choix. Lorsque vous partagez une application avec des utilisateurs externes, vous ne savez pas toujours à l’avance qui aura besoin d’y accéder. Avec l’[inscription en libre-service](../external-identities/self-service-sign-up-overview.md), vous pouvez autoriser les utilisateurs invités à s’inscrire et à obtenir un compte invité pour vos applications métier. Le flux d’inscription peut être créé et personnalisé pour prendre en charge les identités Azure AD et celles des réseaux sociaux. Vous pouvez également collecter des informations supplémentaires sur l’utilisateur lors de l’inscription.

---

 ### <a name="conditional-access-insights-and-reporting-workbook-is-generally-available"></a>Disponibilité générale du classeur Insights et rapports sur l’accès conditionnel

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités

Le [classeur Insights et rapports](../conditional-access/howto-conditional-access-insights-reporting.md) donne aux administrateurs une vue récapitulative de l’accès conditionnel Azure AD dans leur locataire. Avec la possibilité de sélectionner une stratégie individuelle, les administrateurs peuvent mieux comprendre ce que fait chaque stratégie et surveiller les modifications en temps réel. Le classeur diffuse les données stockées dans Azure Monitor, que vous pouvez configurer en quelques minutes en [suivant ces instructions](../reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md). Pour améliorer la visibilité du tableau de bord, nous avons déplacé celui-ci vers le nouvel onglet Insights et rapports dans le menu de l’accès conditionnel Azure AD.

---

### <a name="policy-details-blade-for-conditional-access-is-in-public-preview"></a>Le panneau Détails de la stratégie pour l’accès conditionnel est en préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Accès conditionnel  
**Fonctionnalité de produit :** Protection et sécurité des identités

Le nouveau [panneau Détails de la stratégie](../conditional-access/troubleshoot-conditional-access.md) affiche les affectations, conditions et contrôles qui ont été respectés lors de l’évaluation de la stratégie d’accès conditionnel. Vous pouvez accéder au panneau en sélectionnant une ligne sous les onglets Accès conditionnel ou Rapport seul des Détails de connexion.

---

### <a name="new-query-capabilities-for-directory-objects-in-microsoft-graph-are-in-public-preview"></a>De nouvelles fonctionnalités de requête pour les objets d’annuaire dans Microsoft Graph sont en préversion publique

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** MS Graph **Fonctionnalité de produit :** Expérience de développement

De nouvelles fonctionnalités sont introduites pour les API des objets d’annuaire de Microsoft Graph, ce qui permet d’effectuer des opérations de comptage, de recherche, de filtrage et de tri. Les développeurs pourront ainsi interroger rapidement nos objets d’annuaire sans recourir à des solutions de contournement, telles que les filtrage et tri en mémoire. Apprenez-en davantage dans ce [billet de blog](https://aka.ms/CountFilterMSGraphAAD).

Nous sommes actuellement en préversion publique et aimerions avoir votre avis sur ce point. Merci de nous transmettre vos commentaires en répondant à ce [court sondage](https://aka.ms/MsGraphAADSurveyDocs).

---

### <a name="configure-saml-based-single-sign-on-using-microsoft-graph-api-beta"></a>Configurer l’authentification unique SAML à l’aide de l’API Microsoft Graph (Bêta)

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** SSO
 
La prise en charge de la création et de la configuration d’une application depuis la galerie Azure AD, à l’aide des API Microsoft Graph dans la version Bêta, est désormais disponible. Si vous avez besoin de configurer l’authentification unique SAML pour plusieurs instances d’une application, gagnez du temps en utilisant les API Microsoft Graph pour [automatiser la configuration de l’authentification unique SAML](/graph/application-saml-sso-configure-api).
 
---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---may-2020"></a>Nouveaux connecteurs de provisionnement dans la galerie d’applications Azure AD - Mai 2020

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Intégration tierce
 
Vous pouvez désormais automatiser la création, la mise à jour et la suppression de comptes d’utilisateur pour ces applications nouvellement intégrées :

* [8x8](../saas-apps/8x8-provisioning-tutorial.md)
* [Juno Journey](../saas-apps/juno-journey-provisioning-tutorial.md)
* [MediusFlow](../saas-apps/mediusflow-provisioning-tutorial.md)
* [New Relic by Organization](../saas-apps/new-relic-by-organization-provisioning-tutorial.md)
* [Oracle Cloud Infrastructure Console](../saas-apps/oracle-cloud-infratstructure-console-provisioning-tutorial.md)

Pour découvrir comment sécuriser plus efficacement votre organisation à l’aide de l’approvisionnement automatique de comptes utilisateur, voir [Automatisation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure AD](../app-provisioning/user-provisioning.md).

---

### <a name="saml-token-encryption-is-generally-available"></a>Disponibilité générale du chiffrement de jeton SAML

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** SSO
 
Le [chiffrement de jeton SAML](../manage-apps/howto-saml-token-encryption.md) permet aux applications d’être configurées pour recevoir des assertions SAML chiffrées. La fonctionnalité est désormais en disponibilité générale dans tous les clouds.
 
---

### <a name="group-name-claims-in-application-tokens-is-generally-available"></a>Disponibilité générale des revendications de nom de groupe dans les jetons d’application

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Applications d’entreprise  
**Fonctionnalité de produit :** SSO
 
Les revendications de groupe émises dans un jeton peuvent maintenant être limitées aux seuls groupes attribués à l’application.  Cela est particulièrement important lorsque les utilisateurs sont membres d’un grand nombre de groupes, et qu’il existe un risque de dépassement des limites de taille des jetons. Avec cette nouvelle capacité en place, la possibilité d’[ajouter des noms de groupe à des jetons](../hybrid/how-to-connect-fed-group-claims.md) est mise en disponibilité générale.
 
---

### <a name="workday-writeback-now-supports-setting-work-phone-number-attributes"></a>Workday Writeback prend désormais en charge la définition d’attributs de numéro de téléphone professionnel

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Provisionnement d’applications  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
Nous avons amélioré l’application de provisionnement Workday Writeback pour qu’elle prenne dorénavant en charge la réécriture des attributs de numéros de téléphone mobile et fixe professionnels. Outre l’e-mail et le nom d’utilisateur, vous pouvez à présent configurer l’application de provisionnement Workday Writeback pour transmettre des valeurs de numéro de téléphone d’Azure AD à Workday. Pour plus d’informations sur la configuration de la réécriture des numéros de téléphone, reportez-vous au tutoriel de l’application [Workday Writeback](../saas-apps/workday-writeback-tutorial.md). 

---

### <a name="publisher-verification-preview"></a>Vérification de l’éditeur (préversion)

**Type :** Nouvelle fonctionnalité  
**Catégorie de service :** Autres  
**Fonctionnalité de produit :** Expérience de développement
 
La vérification de l'éditeur (préversion) permet aux administrateurs et aux utilisateurs finaux de s'assurer de l'authenticité des développeurs d'applications qui s'intègrent à la Plateforme d'identités Microsoft. Pour plus d’informations, reportez-vous à [Vérification de l’éditeur (préversion)](../develop/publisher-verification-overview.md).
 
---

### <a name="authorization-code-flow-for-single-page-apps"></a>Flux du code d’autorisation pour les applications à page unique

**Type :** Fonctionnalité modifiée **Catégorie de service :** Authentification **Fonctionnalité de produit :** Expérience de développement

Du fait [des restrictions sur les cookies tiers dans les navigateurs modernes, telles que ITP de Safari](../develop/reference-third-party-cookies-spas.md), les application à page unique (SPA) doivent utiliser le flux du code d’autorisation, plutôt que le flux implicite, pour maintenir l’authentification unique. MSAL.js v 2.x prend désormais en charge le flux du code d’autorisation. Des mises à jour correspondantes étant présentes sur le portail Azure, vous pouvez actualiser votre SPA pour qu’il soit de type « spa » et utilise le flux du code d’authentification. Pour obtenir des instructions, reportez-vous à [Démarrage rapide : Connecter des utilisateurs et obtenir un jeton d’accès dans une application à page unique JavaScript à l’aide du flux de code d’authentification](../develop/quickstart-v2-javascript-auth-code.md).

---

### <a name="improved-filtering-for-devices-is-in-public-preview"></a>Le filtrage amélioré des appareils est en préversion publique

**Type :** Fonctionnalité modifiée   
**Catégorie de service :** Gestion des appareils **Fonctionnalité de produit :** Gestion du cycle de vie des appareils
 
Auparavant, les seuls filtres que vous pouviez utiliser étaient « Enabled » (Activé) et « Activity date » (Date d’activité). À présent, vous pouvez [filtrer votre liste d’appareils sur plus de propriétés](../devices/device-management-azure-portal.md#device-list-filtering-preview), y compris le type de système d’exploitation, le type de jointure, la conformité, etc. Ces ajouts doivent simplifier la localisation d’un appareil particulier.

---

### <a name="the-new-app-registrations-experience-for-azure-ad-b2c-is-now-generally-available"></a>La nouvelle expérience d’inscriptions d’applications pour Azure AD B2C est désormais en disponibilité générale

**Type :** Fonctionnalité modifiée   
**Catégorie de service :** B2C - Gestion des identités consommateurs  
**Fonctionnalité de produit :** Gestion du cycle de vie des identités
 
La nouvelle expérience d’inscriptions d’applications pour Azure AD B2C est désormais en disponibilité générale. 

Auparavant, vous deviez gérer vos applications B2C destinées aux consommateurs séparément du reste de vos applications, en utilisant l’expérience « Applications » héritée. Cela signifiait différentes expériences de création d’applications à différents emplacements dans Azure.

La nouvelle expérience affiche toutes les inscriptions d’applications Azure AD B2C et les inscriptions d’applications Azure AD dans un même emplacement, et permet de les gérer de manière cohérente. Que vous deviez gérer une application accessible aux clients, ou une application qui accède à Microsoft Graph pour manager par programmation des ressources Azure AD B2C, vous n’avez besoin d’apprendre qu’une seule façon de faire les choses.

Vous pouvez afficher la nouvelle expérience en accédant au service Azure AD B2C et en sélectionnant le panneau d’inscriptions des applications. L’expérience est également accessible à partir du service Azure Active Directory.

L’expérience d’inscriptions d’applications Azure AD B2C repose sur l’[expérience d’inscription d’applications générale](https://developer.microsoft.com/identity/blogs/new-app-registrations-experience-is-now-generally-available/) pour les locataires Azure AD, mais elle est personnalisée pour Azure AD B2C. L’expérience « Applications » héritée sera dépréciée à l’avenir.

Pour plus d’informations, consultez [La nouvelle expérience d’inscription d’applications pour Azure AD B2C](../../active-directory-b2c/app-registrations-training-guide.md).

---

## <a name="april-2020"></a>Avril 2020

### <a name="combined-security-info-registration-experience-is-now-generally-available"></a>L’expérience d’inscription combinées des informations de sécurité est désormais généralement disponible

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Authentifications (connexions)

**Fonctionnalité de produit :** Protection et sécurité des identités

L’expérience d’inscription combinée pour l’authentification multifacteur (MFR, Multi-Factor Authentication) et la réinitialisation de mot de passe en libre-service (SSPR, Self-Service Password Reset) est désormais généralement disponible. Cette nouvelle expérience d’inscription permet aux utilisateurs de s’inscrire pour la MFA et la SSPR en un seul processus pas à pas. Lorsque vous déployez la nouvelle expérience pour votre organisation, les utilisateurs peuvent s’inscrire en moins de temps et avec moins de tracas. Consultez le billet de blog [ici](https://bit.ly/3etiRyQ).

---

### <a name="continuous-access-evaluation"></a>Évaluation continue de l’accès

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Authentifications (connexions)

**Fonctionnalité de produit :** Protection et sécurité des identités

L’évaluation continue de l’accès est une nouvelle fonctionnalité de sécurité qui permet une mise en œuvre en quasi-temps réel de stratégies sur des parties se fiant à l’utilisation des jetons d’accès Azure AD lorsque certains événements tels que la suppression d’un compte d’utilisateur se produisent dans Azure AD. Nous déployons cette fonctionnalité en priorité pour les clients Teams et Outlook. Pour plus d’informations, consultez notre [blog](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/moving-towards-real-time-policy-and-security-enforcement/ba-p/1276933) et la [documentation](../conditional-access/concept-continuous-access-evaluation.md).

---

### <a name="sms-sign-in-firstline-workers-can-sign-in-to-azure-ad-backed-applications-with-their-phone-number-and-no-password"></a>Connexion SMS : Les employés de terrain peuvent se connecter à des applications adossées à Azure AD sans introduire de mot de passe, mais simplement leur numéro de téléphone

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Authentifications (connexions)

**Fonctionnalité de produit :** Authentification utilisateur

Office lance une série d’applications métier avant tout mobiles qui s’adressent à des organisations non traditionnelles et à des employés de grandes organisations pour qui l’e-mail n’est pas la méthode de communication principale. Ces applications ciblent les employés de terrain, les travailleurs sans bureau, les agents de terrain ou les effectifs de vente au détail qui n’ont pas forcément d’adresse e-mail professionnelle, ou d’accès à un ordinateur ou à d’autres ressources informatiques. Ce projet permet à ces employés de se connecter à des applications d’entreprise en entrant un numéro de téléphone et un code. Pour en savoir, consultez notre [documentation administrateur](../authentication/howto-authentication-sms-signin.md) et notre [documentation utilisateur final](../user-help/sms-sign-in-explainer.md).

---

### <a name="invite-internal-users-to-use-b2b-collaboration"></a>Inviter les utilisateurs internes à adopter B2B Collaboration

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** B2B

**Fonctionnalité de produit :**

Nous développons la fonctionnalité d’invitation B2B permettant d’inviter des comptes internes existants à utiliser désormais des informations d’identification pour la collaboration B2B. Pour ce faire, vous pouvez transmettre l’objet utilisateur à l’API Invite en plus de paramètres standard tels que l’adresse e-mail invitée. L’ID d’objet, l’UPN, l’appartenance à un groupe, l’affectation d’applications et autres informations des utilisateurs restent intacts, mais ceux-ci utilisent désormais la solution B2B pour s’authentifier avec les informations d’identification de leur locataire de base plutôt qu’avec les informations d’identification internes qu’ils utilisaient avant l’invitation. Pour plus de détails, consultez la [documentation](../external-identities/invite-internal-users.md).

---

### <a name="report-only-mode-for-conditional-access-is-now-generally-available"></a>Disponibilité générale du mode rapport seul pour l’accès conditionnel

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Accès conditionnel

**Fonctionnalité de produit :** Protection et sécurité des identités

Le [mode rapport seul pour l’accès conditionnel Azure AD](../conditional-access/concept-conditional-access-report-only.md) vous permet d’évaluer le résultat d’une stratégie sans appliquer de contrôles d’accès. Vous pouvez tester les stratégies de rapport seul au sein de votre organisation afin de bien comprendre leur impact avant de les activer, ce qui rend leur déploiement à la fois plus sûr et plus facile. Ces derniers mois, nous avons constaté une adoption forte du mode rapport seul, avec plus de 26 millions d’utilisateurs opérant déjà dans le cadre d’une stratégie de rapport seul. À la suite de cette annonce, les nouvelles stratégies d’accès conditionnel Azure AD seront créées par défaut en mode rapport seul. Cela signifie que vous pouvez surveiller l’impact de vos stratégies à partir du moment de leur création. Et ceux d’entre vous qui utilisent les API MS Graph peuvent également [gérer les stratégies de rapport seul par programmation](/graph/api/resources/conditionalaccesspolicy?view=graph-rest-beta). 

---

### <a name="conditional-access-insights-and-reporting-workbook-is-generally-available"></a>Disponibilité générale du classeur Insights et rapports de l’accès conditionnel

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Accès conditionnel

**Fonctionnalité de produit :** Protection et sécurité des identités

Le [classeur Insights et rapports](../conditional-access/howto-conditional-access-insights-reporting.md) de l’accès conditionnel donne aux administrateurs une vue récapitulative de l’accès conditionnel Azure AD dans leur locataire. Avec la possibilité de sélectionner une stratégie individuelle, les administrateurs peuvent mieux comprendre ce que fait chaque stratégie et surveiller les modifications en temps réel. Le classeur diffuse les données stockées dans Azure Monitor, que vous pouvez configurer en quelques minutes en [suivant ces instructions](../reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md). Pour améliorer la visibilité du tableau de bord, nous avons déplacé celui-ci vers le nouvel onglet Insights et rapports dans le menu de l’accès conditionnel Azure AD.

---

### <a name="policy-details-blade-for-conditional-access-is-in-public-preview"></a>Le panneau Détails de la stratégie pour l’accès conditionnel est en préversion publique

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Accès conditionnel

**Fonctionnalité de produit :** Protection et sécurité des identités

Le nouveau [panneau Détails de la stratégie](../conditional-access/troubleshoot-conditional-access.md) affiche les affectations, conditions et contrôles qui ont été respectés lors de l’évaluation de la stratégie d’accès conditionnel. Vous pouvez accéder au panneau en sélectionnant une ligne sous les onglets **Accès conditionnel** ou **Rapport seul** des Détails de connexion.

---

### <a name="new-federated-apps-available-in-azure-ad-app-gallery---april-2020"></a>Nouvelles applications fédérées disponibles dans la galerie d’applications Azure AD - Avril 2020

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Applications d’entreprise

**Fonctionnalité de produit :** Intégration tierce

En avril 2020, nous avons ajouté à la galerie d’applications les 31 nouvelles applications suivantes qui prennent en charge la fédération des identités : 

[SincroPool Apps](https://www.sincropool.com/), [SmartDB](https://hibiki.dreamarts.co.jp/smartdb/trial/), [Float](../saas-apps/float-tutorial.md), [LMS365](https://lms.365.systems/), [IWT Procurement Suite](../saas-apps/iwt-procurement-suite-tutorial.md), [Lunni](https://lunni.fi/), [EasySSO for Jira](../saas-apps/easysso-for-jira-tutorial.md), [Virtual Training Academy](https://vta.c3p.ca/app/en/openid?authenticate_with=microsoft), [Meraki Dashboard](../saas-apps/meraki-dashboard-tutorial.md), [Microsoft 365 Mover](https://app.mover.io/login), [Speaker Engage](https://speakerengage.com/login.php), [Honestly](../saas-apps/honestly-tutorial.md), [Ally](../saas-apps/ally-tutorial.md), [DutyFlow](https://app.dutyflow.nl/), [AlertMedia](../saas-apps/alertmedia-tutorial.md), [gr8 People](../saas-apps/gr8-people-tutorial.md), [Pendo](../saas-apps/pendo-tutorial.md), [HighGround](../saas-apps/highground-tutorial.md), [Harmony](../saas-apps/harmony-tutorial.md), [Timetabling Solutions](../saas-apps/timetabling-solutions-tutorial.md), [SynchroNet CLICK](../saas-apps/synchronet-click-tutorial.md), [empower](https://www.made-in-office.com/en/), [Fortes Change Cloud](../saas-apps/fortes-change-cloud-tutorial.md), [Litmus](../saas-apps/litmus-tutorial.md), [GroupTalk](https://recorder.grouptalk.com/), [Frontify](../saas-apps/frontify-tutorial.md), [MongoDB Cloud](../saas-apps/mongodb-cloud-tutorial.md), [TickitLMS Learn](../saas-apps/tickitlms-learn-tutorial.md), [COCO](https://hexaware.com/partnerships-and-alliances/digital-transformation-using-microsoft-azure/), [Nitro Productivity Suite](../saas-apps/nitro-productivity-suite-tutorial.md) , [Trend Micro Web Security(TMWS)](https://review.docs.microsoft.com/azure/active-directory/saas-apps/trend-micro-tutorial)

Pour plus d’informations sur les applications, consultez [Intégration des applications SaaS à Azure Active Directory](../saas-apps/tutorial-list.md). Pour plus d’informations sur le référencement de votre application dans la galerie Azure AD App, consultez [Lister votre application dans la galerie d’applications Azure Active Directory](../azuread-dev/howto-app-gallery-listing.md).

---

### <a name="microsoft-graph-delta-query-support-for-oauth2permissiongrant-available-for-public-preview"></a>Disponibilité de la prise en charge de requête delta Microsoft Graph pour oAuth2PermissionGrant en préversion publique

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** MS Graph

**Fonctionnalité de produit :** Expérience de développement

La requête delta pour oAuth2PermissionGrant est disponible en préversion publique. Vous pouvez maintenant suivre des modifications sans devoir continuellement interroger Microsoft Graph. [En savoir plus.](/graph/api/oAuth2PermissionGrant-delta?tabs=http&view=graph-rest-beta)

---

### <a name="microsoft-graph-delta-query-support-for-organizational-contact-generally-available"></a>Disponibilité générale de la prise en charge de requête delta Microsoft Graph pour les contacts professionnels

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** MS Graph

**Fonctionnalité de produit :** Expérience de développement

La requête delta pour les contacts professionnels est en disponibilité générale. Vous pouvez à présent suivre les modifications dans les applications de production sans devoir interroger continuellement Microsoft Graph. Remplacez tout code interrogeant continuellement les données orgContact par une requête delta afin d’améliorer considérablement les performances. [En savoir plus.](/graph/api/orgcontact-delta?tabs=http&view=graph-rest-1.0)

---

### <a name="microsoft-graph-delta-query-support-for-application-generally-available"></a>Disponibilité générale de la prise en charge de requête delta Microsoft Graph pour les applications

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** MS Graph

**Fonctionnalité de produit :** Expérience de développement

La requête delta pour les applications est généralement disponible. Vous pouvez maintenant suivre les modifications dans les applications de production sans devoir interroger continuellement Microsoft Graph. Remplacez tout code interrogeant continuellement les données d’application par une requête delta afin d’améliorer considérablement les performances. [En savoir plus.](/graph/api/application-delta?view=graph-rest-1.0)

---

### <a name="microsoft-graph-delta-query-support-for-administrative-units-available-for-public-preview"></a>Disponibilité de la prise en charge de requête delta Microsoft Graph pour les unités administratives en préversion publique

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** MS Graph

**Fonctionnalité de produit :** La requête delta de l’expérience développeur pour les unités administratives est disponible en préversion publique. Vous pouvez maintenant suivre des modifications sans devoir continuellement interroger Microsoft Graph. [En savoir plus.](/graph/api/administrativeunit-delta?tabs=http&view=graph-rest-beta)

---

### <a name="manage-authentication-phone-numbers-and-more-in-new-microsoft-graph-beta-apis"></a>Gestion des numéros de téléphone d’authentification et bien plus encore dans les nouvelles API bêta de Microsoft Graph

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** MS Graph

**Fonctionnalité de produit :** Expérience de développement

Ces API constituent un outil essentiel pour la gestion des méthodes d’authentification de vos utilisateurs. Vous pouvez désormais préinscrire et gérer par programme les authentificateurs utilisés pour l’authentification multifacteur et la réinitialisation de mot de passe en libre-service. Il s’agit de l’une des fonctionnalités les plus demandées dans les espaces Azure MFA, SSPR et Microsoft Graph. Les nouvelles API que nous avons publiées dans cette vague vous donnent la possibilité d’effectuer les opérations suivantes :

- Lire, ajouter, mettre à jour et supprimer les téléphones d’authentification d’un utilisateur
- Réinitialiser le mot de passe d’un utilisateur
- Activer et désactiver la connexion par SMS

Pour plus d’informations, consultez [Présentation de l’API Méthodes d’authentification Azure AD](/graph/api/resources/authenticationmethods-overview?view=graph-rest-beta).

---

### <a name="administrative-units-public-preview"></a>Préversion publique des unités administratives

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Rôles Azure AD

**Fonctionnalité de produit :** Contrôle d’accès

Les unités administratives vous permettent d’accorder des autorisations d’administrateur limitées à un service, une région ou un autre segment de votre organisation que vous définissez. Vous pouvez utiliser des unités administratives pour déléguer des autorisations à des administrateurs régionaux ou définir une stratégie à un niveau précis. Par exemple, un administrateur de comptes d’utilisateur peut mettre à jour des informations de profil, réinitialiser des mots de passe et attribuer des licences aux utilisateurs uniquement dans son unité administrative.

Les unités administratives permettent à un administrateur central d’effectuer les opérations suivantes :

- Créer une unité administrative pour la gestion décentralisée des ressources
- Attribuer un rôle disposant d’autorisations administratives uniquement sur les utilisateurs Azure AD d’une unité administrative
- Remplir les unités administratives d’utilisateurs et de groupes en fonction des besoins

Pour plus d’informations, consultez [Gestion des unités administratives dans Azure Active Directory (préversion)](../users-groups-roles/directory-administrative-units.md)

---

### <a name="printer-administrator-and-printer-technician-built-in-roles"></a>Rôles intégrés Administrateur d’imprimantes et Technicien en charge des imprimantes

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Rôles Azure AD

**Fonctionnalité de produit :** Contrôle d’accès

**Administrateur d’imprimantes**  : Les utilisateurs ayant ce rôle peuvent inscrire des imprimantes et gérer tous les aspects liés aux configurations de celles-ci dans la solution Impression universelle de Microsoft, dont les paramètres du connecteur d’impression universelle. Ils peuvent consentir à toutes les demandes d’autorisation d’impression déléguée. Les administrateurs d’imprimantes ont également accès aux rapports d’impression. 

**Technicien en charge des imprimantes**  : Les utilisateurs ayant ce rôle peuvent inscrire des imprimantes et gérer leur statut dans la solution Impression universelle de Microsoft. Ils peuvent également lire toutes les informations du connecteur. L’une des tâches clés qu’un technicien en charge des imprimantes ne peut pas accomplir est la définition d’autorisations utilisateur sur les imprimantes et le partage d’imprimantes. [En savoir plus.](../roles/permissions-reference.md#printer-administrator)

---

### <a name="hybrid-identity-admin-built-in-role"></a>Rôle intégré d’administrateur d’identité hybride

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Rôles Azure AD

**Fonctionnalité de produit :** Contrôle d’accès

Les utilisateurs de ce rôle peuvent activer, configurer et gérer les services et paramètres liés à l’activation de l’identité hybride dans Azure AD. Ce rôle permet de configurer Azure AD sur l’une des trois méthodes d’authentification prises en charge (synchronisation de hachage du mot de passe, authentification directe ou fédération -AD FS ou fournisseur de fédération tiers-), et de déployer une infrastructure locale associée pour les activer. L’infrastructure locale comprend des agents d’approvisionnement et d’authentification directe. Ce rôle donne la possibilité d’activer l’authentification unique transparente (S-SSO) pour permettre une authentification transparente sur des appareils autres que Windows 10 ou des ordinateurs autres que Windows Server 2016. En outre, ce rôle donne la possibilité de voir les journaux de connexion et d’accéder à des informations en lien avec l’intégrité et l’analytique à des fins de surveillance et de dépannage. [En savoir plus.](../roles/permissions-reference.md#hybrid-identity-administrator)

---

### <a name="network-administrator-built-in-role"></a>Rôle intégré d’administrateur réseau

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** Rôles Azure AD

**Fonctionnalité de produit :** Contrôle d’accès

Les utilisateurs titulaires de ce rôle peuvent passer en revue, depuis l’emplacement où ils se trouvent, les recommandations de Microsoft relatives à l’architecture du périmètre réseau, basées sur la télémétrie du réseau. Les performances réseau pour Microsoft 365 s’appuient sur une architecture de périmètre de réseau client entreprise soigneuse, qui est généralement propre à la localisation de l’utilisateur. Ce rôle permet de modifier les emplacements utilisateur découverts et la configuration des paramètres réseau pour ces emplacements afin de faciliter les mesures de télémétrie et les recommandations de conception améliorées. [En savoir plus.](../roles/permissions-reference.md#network-administrator)

---

### <a name="bulk-activity-and-downloads-in-the-azure-ad-admin-portal-experience"></a>Activité en bloc et téléchargements dans l’expérience du portail d’administration Azure AD

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** User Management

**Fonctionnalité de produit :** Répertoire

Vous pouvez désormais conduire des activités en bloc sur des utilisateurs et des groupes dans Azure AD en téléchargeant un fichier CSV via le portail d’administration d’Azure AD. Vous pouvez créer, supprimer et inviter des utilisateurs. Vous pouvez ajouter et supprimer des membres dans un groupe.

Vous pouvez également télécharger des listes de ressources Azure AD à partir du portail d’administration d’Azure AD. Vous pouvez télécharger les listes des utilisateurs et des groupes figurant dans l’annuaire, ainsi que la liste des membres d’un groupe particulier.

Pour plus d’informations, consultez les articles suivants :

- [Créer des utilisateurs](../enterprise-users/users-bulk-add.md) ou [Inviter des utilisateurs](../external-identities/tutorial-bulk-invite.md)
- [Supprimer des utilisateurs](../enterprise-users/users-bulk-delete.md) ou [Restaurer des utilisateurs supprimés](../enterprise-users/users-bulk-restore.md)
- [Télécharger la liste des utilisateurs](../enterprise-users/users-bulk-download.md) ou [Télécharger la liste des groupes](../enterprise-users/groups-bulk-download.md)
- [Ajouter (importer) des membres](../enterprise-users/groups-bulk-import-members.md), [Supprimer des membres](../enterprise-users/groups-bulk-remove-members.md) ou [Télécharger la liste des membres](../enterprise-users/groups-bulk-download-members.md) d’un groupe

---

### <a name="my-staff-delegated-user-management"></a>Gestion des utilisateurs délégués de Mon personnel

**Type :** Nouvelle fonctionnalité

**Catégorie de service :** User Management

**Fonctionnalité de produit :**

Le portail Mon personnel permet aux responsables sur le terrain, tels que des responsables de magasin, de s’assurer que les membres de leur personnel sont en mesure d’accéder à leurs comptes Azure AD. Au lieu de s’appuyer sur un support technique central, les organisations peuvent déléguer à un responsable sur le terrain des tâches courantes telles que la réinitialisation de mot de passe ou la modification de numéros de téléphone. Grâce au portail Mon personnel, un utilisateur qui ne parvient plus à accéder à son compte peut récupérer l’accès en quelques clics, sans intervention du support technique ou du personnel informatique. Pour plus d’informations, consultez [Gestion des utilisateurs avec Mon personnel (préversion)](../users-groups-roles/my-staff-configure.md) et [Déléguer la gestion des utilisateurs avec Mon personnel (préversion)](../user-help/my-staff-team-manager.md).

---

### <a name="an-upgraded-end-user-experience-in-access-reviews"></a>Expérience d’utilisateur final mise à niveau dans les révisions d’accès

**Type :** Fonctionnalité modifiée

**Catégorie de service :** Révisions d’accès

**Fonctionnalité de produit :** Gouvernance des identités

Nous avons mis à jour l’expérience du réviseur pour les révisions d’accès Azure AD dans le portail Mes applications. Depuis la fin du mois d’avril, les réviseurs connectés à l’interface réviseur des révisions d’accès Azure AD voient s’afficher une bannière qui leur permet d’essayer l’expérience mise à jour dans le portail Mon accès. Notez que l’expérience des révisions d’accès mise à jour offre les mêmes fonctionnalités que l’expérience antérieure, mais avec une interface utilisateur améliorée s’ajoutant aux nouvelles fonctionnalités pour permettre aux utilisateurs d’être productifs. [Vous pouvez en savoir plus sur l’expérience mise à jour ici](../governance/perform-access-review.md). Cette préversion publique sera disponible jusqu’à la fin du mois de juillet 2020. À partir de cette date, les réviseurs qui n’auront pas adopté l’expérience en préversion seront automatiquement dirigés vers le portail Mon accès pour effectuer des révisions d’accès. Si vous souhaitez que vos réviseurs basculent définitivement vers l’expérience en préversion dans le portail Mon accès dès maintenant, [veuillez introduire une demande ici](https://forms.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR5dv-S62099HtxdeKIcgO-NUOFJaRDFDWUpHRk8zQ1BWVU1MMTcyQ1FFUi4u).

---

### <a name="workday-inbound-user-provisioning-and-writeback-apps-now-support-the-latest-versions-of-workday-web-services-api"></a>Les applications d’approvisionnement des utilisateurs entrants et d’écriture différée de Workday prennent désormais en charge les dernières versions de l’API Workday Web Services (WWS).

**Type :** Fonctionnalité modifiée

**Catégorie de service :** Provisionnement d’applications

**Fonctionnalité de produit :** 

Sur la base des commentaires des clients, nous avons mis à jour les applications d’approvisionnement des utilisateurs entrants et d’écriture différée de Workday dans la galerie d’applications d’entreprise pour prendre en charge les dernières versions de l’API Workday Web Services (WWS). Suite à cette modification, les clients peuvent spécifier la version de l’API WWS qu’ils souhaitent utiliser dans la chaîne de connexion. Les clients peuvent ainsi récupérer davantage d’attributs de RH disponibles dans les versions de Workday. L’application d’écriture différée de Workday utilise désormais le service web recommandé Change_Work_Contact_Info de Workday pour surmonter les limitations de Maintain_Contact_Info.

Si aucune version n’est spécifiée dans la chaîne de connexion, par défaut, les applications d’approvisionnement entrant de Workday continueront d’utiliser WWS v 21.1. Pour basculer vers les dernières API Workday pour l’approvisionnement d’utilisateurs entrants, les clients doivent mettre à jour la chaîne de connexion comme indiqué [dans le didacticiel](../saas-apps/workday-inbound-tutorial.md#which-workday-apis-does-the-solution-use-to-query-and-update-workday-worker-profiles), et mettre à jour les XPATH utilisés pour les attributs Workday, comme décrit dans le [Guide de référence sur les attributs Workday](../app-provisioning/workday-attribute-reference.md#xpath-values-for-workday-web-services-wws-api-v30). 

Pour utiliser la nouvelle API pour l’écriture différée, aucune modification n’est requise dans l’application d’approvisionnement d’écriture différée de Workday. Du côté de Workday, assurez-vous que le compte d’utilisateur de système d’intégration (ISU) de Workday dispose des autorisations nécessaires pour appeler le processus métier Change_Work_Contact comme indiqué dans la section [Configurer des autorisations de stratégie de sécurité de processus métier](../saas-apps/workday-inbound-tutorial.md#configuring-business-process-security-policy-permissions) du didacticiel. 

Nous avons mis à jour notre [didacticiel](../saas-apps/workday-inbound-tutorial.md) pour refléter la prise en charge de la nouvelle version de l’API.

---

### <a name="users-with-default-access-role-are-now-in-scope-for-provisioning"></a>Utilisateurs titulaires du rôle d’accès par défaut désormais dans l’étendue de l’approvisionnement

**Type :** Fonctionnalité modifiée

**Catégorie de service :** Provisionnement d’applications

**Fonctionnalité de produit :** Gestion du cycle de vie des identités

Historiquement, les utilisateurs pourvus du rôle d’accès par défaut étaient hors de portée du provisionnement. Certains clients souhaitaient que les utilisateurs disposant de ce rôle figurent dans l’étendue du provisionnement. Depuis le 16 avril 2020, toutes les nouvelles configurations d’approvisionnement permettent d’approvisionner les utilisateurs titulaires du rôle d’accès par défaut. Progressivement, nous allons modifier le comportement des configurations d’approvisionnement existantes pour prendre en charge l’approvisionnement d’utilisateurs avec ce rôle. [En savoir plus.](../app-provisioning/application-provisioning-config-problem-no-users-provisioned.md)

---

### <a name="updated-provisioning-ui"></a>IU d’approvisionnement mise à jour

**Type :** Fonctionnalité modifiée

**Catégorie de service :** Provisionnement d’applications

**Fonctionnalité de produit :** Gestion du cycle de vie des identités

Nous avons actualisé notre expérience d’approvisionnement pour créer une vue de gestion plus ciblée. Lorsque vous accédez au panneau d’approvisionnement d’une application d’entreprise déjà configurée, vous pouvez facilement surveiller la progression de l’approvisionnement et gérer des actions telles que le démarrage, l’arrêt et le redémarrage de l’approvisionnement. [En savoir plus.](../app-provisioning/configure-automatic-user-provisioning-portal.md)

---

### <a name="dynamic-group-rule-validation-is-now-available-for-public-preview"></a>Validation de règle de groupe dynamique désormais disponible en préversion publique

**Type :** Fonctionnalité modifiée

**Catégorie de service :** Gestion des groupes

**Fonctionnalité de produit :** Collaboration

Azure Active Directory (Azure AD) offre désormais la possibilité de valider les règles de groupe dynamique. Sous l’onglet **Valider les règles** , vous pouvez valider votre règle dynamique par rapport à des exemples de membres du groupe pour vérifier que la règle fonctionne comme prévu. Lors de la création ou de la mise à jour des règles de groupe dynamiques, les administrateurs veulent savoir si un utilisateur ou un appareil sera membre du groupe. Cela permet d’évaluer si un utilisateur ou un appareil répond aux critères de la règle et facilite la résolution des problèmes quand l’appartenance n’est pas attendue.

Pour plus d’informations, consultez [Valider une règle d’appartenance à un groupe dynamique (préversion)](../enterprise-users/groups-dynamic-rule-validation.md).

---

### <a name="identity-secure-score---security-defaults-and-mfa-improvement-action-updates"></a>Score d’identité sécurisée – Mises à jour des actions d’amélioration des paramètres de sécurité par défaut et de l’authentification multifacteur

**Type :** Fonctionnalité modifiée

**Catégorie de service :** N/A

**Fonctionnalité de produit :** Protection et sécurité des identités

**Prise en charge des paramètres de sécurité par défaut pour les actions d’amélioration d’Azure AD :** Le service Degré de sécurisation Microsoft mettra à jour les actions d’amélioration pour prendre en charge les [paramètres de sécurité par défaut dans Azure AD](./concept-fundamentals-security-defaults.md), facilitant la protection de votre organisation à l’aide de paramètres de sécurité préconfigurés pour contrer des attaques courantes. Cela aura une incidence sur les actions d’amélioration suivantes :

- Vérifier que tous les utilisateurs peuvent utiliser une authentification multifacteur pour un accès sécurisé
- Exiger l'authentification multifacteur pour les rôles administratifs
- Activer une stratégie pour bloquer l’authentification héritée
 
**Mises à jour de l’action d’amélioration de l’authentification multifacteur :** Afin de refléter la nécessité pour les entreprises de garantir une sécurité optimale tout en appliquant des stratégies adaptées à leur activité, le service Degré de sécurisation Microsoft a supprimé trois actions d’amélioration centrées sur l’authentification multifacteur, et en a ajouté deux.

Actions d’amélioration supprimées :

- Inscrire tous les utilisateurs pour l’authentification multifacteur
- Exiger MFA pour tous les utilisateurs
- Exiger l'authentification multifacteur pour les rôles privilégiés Azure AD

Actions d’amélioration ajoutées :

- Vérifier que tous les utilisateurs peuvent utiliser une authentification multifacteur pour un accès sécurisé
- Exiger l'authentification multifacteur pour les rôles administratifs

Ces nouvelles actions d’amélioration nécessitent l’inscription de vos utilisateurs ou administrateurs pour l’authentification multifacteur dans votre annuaire, ainsi que la mise en place d’un ensemble approprié de stratégies adaptées aux besoins de votre organisation. L'objectif principal est de disposer d'une certaine flexibilité tout en permettant à l'ensemble de vos utilisateurs et administrateurs de s'authentifier à l'aide de plusieurs facteurs ou d'invites de vérification d'identité basée sur les risques. Cela peut prendre la forme de l’instauration de plusieurs stratégies qui appliquent des décisions étendues ou de la définition de paramètres de sécurité par défaut (à compter du 16 mars) qui permettent à Microsoft de décider quand exiger l’authentification multifacteur des utilisateurs. [En savoir plus sur les nouveautés du service Degré de sécurisation Microsoft](/microsoft-365/security/mtp/microsoft-secure-score?view=o365-worldwide#whats-new).

---