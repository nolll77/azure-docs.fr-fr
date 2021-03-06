---
title: Renouveler un certificat Azure Application Gateway
description: Découvrez comment renouveler un certificat associé à un écouteur de passerelle Application Gateway.
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: how-to
ms.date: 8/15/2018
ms.author: victorh
ms.openlocfilehash: de57a58f7c891009d2e0cc43b351c2cad42a2766
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "84807886"
---
# <a name="renew-application-gateway-certificates"></a>Renouveler des certificats Application Gateway

À un moment donné, vous devrez renouveler vos certificats si vous avez configuré votre passerelle Application Gateway pour le chiffrement TLS/SSL.

Vous pouvez renouveler un certificat associé à un écouteur à l’aide du Portail Azure, d’Azure PowerShell ou d’Azure CLI :

## <a name="azure-portal"></a>Portail Azure

Pour renouveler un certificat d’écouteur à partir du portail, accédez à vos écouteurs Application Gateway. Cliquez sur l’écouteur dont vous devez renouveler le certificat, puis cliquez sur **Renew or edit selected certificate** (Renouveler ou modifier le certificat sélectionné).

![Renouvellement de certificat](media/renew-certificate/ssl-cert.png)

Chargez votre nouveau certificat PFX, attribuez-lui un nom, tapez le mot de passe, puis cliquez sur **Enregistrer**.

## <a name="azure-powershell"></a>Azure PowerShell

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

Pour renouveler votre certificat à l’aide d’Azure PowerShell, utilisez le script suivant :

```azurepowershell-interactive
$appgw = Get-AzApplicationGateway `
  -ResourceGroupName <ResourceGroup> `
  -Name <AppGatewayName>

$password = ConvertTo-SecureString `
  -String "<password>" `
  -Force `
  -AsPlainText

set-AzApplicationGatewaySSLCertificate -Name <oldcertname> `
-ApplicationGateway $appgw -CertificateFile <newcertPath> -Password $password

Set-AzApplicationGateway -ApplicationGateway $appgw
```
## <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az network application-gateway ssl-cert update \
  -n "<CertName>" \
  --gateway-name "<AppGatewayName>" \
  -g "ResourceGroupName>" \
  --cert-file <PathToCerFile> \
  --cert-password "<password>"
```

## <a name="next-steps"></a>Étapes suivantes

Pour découvrir comment configurer le déchargement TLS avec la passerelle Azure Application Gateway, consultez la [configuration du déchargement TLS](application-gateway-ssl-portal.md)
