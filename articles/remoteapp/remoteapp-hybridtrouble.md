---
title: "aaaTroubleshoot criando coleções do RemoteApp híbrido | Microsoft Docs"
description: "Saiba como falhas na criação de coleção híbrida tootroubleshoot RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Solucionar problemas na criação de coleções híbridas do RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Uma coleção híbrida é hospedada no e armazena dados em Olá nuvem do Azure, mas também permite que usuários acessem dados e recursos armazenados em sua rede local. Os usuários podem acessar aplicativos ao efetuar logon com suas credenciais corporativas sincronizadas ou federadas com o Active Directory do Azure. Você pode implantar uma coleção híbrida que usa uma Rede Virtual existente do Azure, ou você pode criar uma nova rede virtual. Recomendamos que você crie ou use uma sub-rede da rede virtual com uma variedade CIDR grande o suficiente para futuro crescimento estimado para o RemoteApp do Azure.

Ainda não criou sua coleção? Consulte [criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md) para etapas de saudação.

Se você estiver tendo problemas para criar sua coleção, ou se não estiver funcionando, coleção Olá maneira Olá achar que deve, confira Olá informações a seguir.

## <a name="your-image-is-invalid"></a>A imagem é inválida
Se você vir uma mensagem como "GoldImageInvalid" quando você está esperando por Azure tooprovision sua coleção, isso significa que a imagem de modelo não atende a saudação [definido requisitos de imagem](remoteapp-imagereqs.md). Assim, vá ler os [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente toocreate sua coleção novamente.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>A sua VNET tem grupos de segurança de rede definidos?
Se você tiver definidos na sub-rede Olá que você está usando para sua coleção de grupos de segurança de rede, verifique se esses [URLs e portas](remoteapp-ports.md) são acessíveis a partir de sua sub-rede.

Você pode adicionar rede adicional segurança grupos toohello VMs implantadas por você na sub-rede Olá para um controle.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Você está usando seus próprios servidores DNS? Eles são acessíveis da sua sub-rede VNET?
> [!NOTE]
> Você tem toomake Olá-se de que os servidores DNS na sua rede virtual estão sempre ativados e sempre capaz tooresolve máquinas de virtuais de Olá hospedadas em redes de saudação. Não use o DNS do Google para isso.
> 
> 

Para coleções híbridas, use seus próprios servidores DNS. Você especificá-los em seu esquema de configuração de rede ou por meio do portal de gerenciamento hello quando você criar sua rede virtual. Servidores DNS são usados na ordem de saudação que elas são especificadas em uma forma de failover (como tooround contrário robin).  
Consulte também[resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake-se de que os servidores DNS estão correcly configurado.

Verifique se os servidores DNS Olá para sua coleção estão acessíveis e disponíveis na sub-rede da rede virtual de saudação especificado para esta coleção.

Por exemplo:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir o DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Você está usando um controlador de domínio do Active Directory em sua coleção?
No momento, somente um domínio do Active Directory pode ser associado ao RemoteApp do Azure. a coleção de híbrida Olá suporta apenas as contas do Active Directory do Azure que foram sincronizadas usando a ferramenta DirSync de uma implantação do Windows Server Active Directory; Especificamente, ou sincronizados com a opção de sincronização de senha Olá sincronizado com a federação de serviços de Federação do Active Directory (AD FS) configurada. Você precisa toocreate um domínio personalizado que coincide com o sufixo de domínio do UPN Olá para seu domínio local e configurar a integração de diretório.

Confira [Configurando o Active Directory para o RemoteApp do Azure](remoteapp-ad.md) para obter informações de planejamento.

Certifique-se de detalhes do domínio Olá fornecidos são válidos e o controlador de domínio Olá é acessível a partir do hello que VM criada na sub-rede Olá usado para o aplicativo remoto do Azure. Verifique também se a conta de serviço Olá credenciais fornecidas têm permissões tooadd computadores toohello desde que o domínio e que Olá nome AD fornecido pode ser resolvida a partir de saudação DNS fornecido na VNET de saudação.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Que nome de domínio você especificou quando criou a sua coleção?
o nome de domínio Olá criado ou adicionado deve ser um nome de domínio interno (não o nome de domínio do AD do Azure) e deve estar no formato DNS resolvido (contoso. local). Por exemplo, você tem um nome interno do Active Directory (contoso. local) e um UPN de diretório ativo (contoso.com) - você tem nome interno do toouse hello quando você cria sua coleção.

