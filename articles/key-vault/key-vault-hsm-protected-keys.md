---
title: aaaHow toogenerate e transferir chaves protegidas por HSM para o Cofre de chaves do Azure | Microsoft Docs
description: "Use toohelp neste artigo, planejar, gerar e transferir sua própria toouse chaves protegidas por HSM com o Cofre de chaves do Azure. Também conhecido como BYOK ou Traga sua própria chave."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Como toogenerate e transferir chaves protegidas por HSM para o Cofre de chaves do Azure
## <a name="introduction"></a>Introdução
Para garantia extra, quando você usar o Cofre de chaves do Azure, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello. Este cenário é geralmente chamado tooas *Traga sua própria chave*, ou BYOK. Olá HSMs são FIPS 140-2 nível 2 validado. Cofre de chaves do Azure usa a família Thales nShield dos HSMs tooprotect suas chaves.

Use as informações de saudação toohelp neste tópico, você planejar, gera e transferir toouse suas próprias chaves protegidas por HSM com o Cofre de chaves do Azure.

Essa funcionalidade não está disponível para o Azure China.

> [!NOTE]
> Para obter mais informações sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)  
>
> Para obter um tutorial de Introdução, que inclui a criação de um Cofre da Chave para chaves de HSM protegido, consulte [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).
>
>

Obter mais informações sobre como gerar e transferir uma chave protegida por HSM pela Olá Internet:

* Você gera a chave de saudação de uma estação de trabalho offline, o que reduz a superfície de ataque de saudação.
* chave de saudação é criptografada com uma chave de troca de chave (KEK), que permanece criptografada até que ele é transferido toohello HSMs do Cofre de chaves do Azure. Apenas Olá versão criptografada da chave de deixa a estação de trabalho original Olá.
* saudação de conjunto de ferramentas define propriedades na chave de locatário que associa sua chave toohello mundo de segurança do Cofre de chaves do Azure. Assim após Olá HSMs do Cofre de chave do Azure receberem e descriptografarem a chave, somente esses HSMs poderão usá-lo. A chave não pode ser exportada. Essa associação é imposta pelo Olá HSMs da Thales.
* Olá chave de troca de chave (KEK) que é usado tooencrypt sua chave é gerada dentro Olá HSMs do Cofre de chave do Azure e não é exportável. Olá HSMs impõem que não pode haver nenhuma versão clara do hello KEK fora Olá HSMs. Além disso, a saudação de conjunto de ferramentas inclui Atestado da Thales que Olá KEK não é exportável e foi gerada dentro de um HSM original que foi fabricado pela Thales.
* saudação de conjunto de ferramentas inclui Atestado da Thales de que Olá mundo de segurança também foi gerado em um HSM original fabricado pela Thales o Cofre de chaves do Azure. Este Atestado prova tooyou que a Microsoft está usando hardware original.
* A Microsoft usa KEKs separadas e separa os universos de segurança em cada região geográfica. Essa separação garante que a chave pode ser usada apenas em data centers na região de saudação em que você criptografou. Por exemplo, uma chave de um cliente europeu não pode ser usada em data centers na América do Norte ou na Ásia.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Para obter mais informações sobre serviços HSMs da Thales e da Microsoft
A Thales e-Security é uma fornecedora líder global de criptografia de dados e cyber segurança soluções toohello serviços financeiros, alta tecnologia, manufatura, governo e setores de tecnologia. Com um 40 anos acompanhar de proteção de informações corporativas e governamentais, as soluções Thales são usadas por quatro das cinco empresas maiores de energia e aeroespacial hello. Suas soluções também são usadas por 22 países da OTAN e protegem mais de 80 porcento das transações de pagamento em todo o mundo.

A Microsoft tem colaborado com estado de saudação do Thales tooenhance de arte HSMs. Essas melhorias permitem benefícios típicos de saudação de tooget de serviços hospedados sem abrir mão do controle sobre as chaves. Especificamente, essas melhorias permitem que a Microsoft gerenciar Olá HSMs para que você não precisa. Como uma nuvem de serviço, o Azure Key Vault é dimensionado a curto prazo toomeet picos de uso da sua organização. AT Olá mesmo tempo, sua chave está protegida dentro dos HSMs da Microsoft: você mantém controle sobre o ciclo de vida Olá porque gerar chave hello e transferi-la HSMs do tooMicrosoft.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Implementando o Traga a sua própria chave (BYOK) para o Cofre da Chave do Azure
Olá use informações e os procedimentos a seguir se você gerar sua própria chave protegida por HSM e transferi-la tooAzure Cofre de chave — Olá traga seu próprio cenário da chave (BYOK).

## <a name="prerequisites-for-byok"></a>Pré-requisitos para BYOK
Consulte o hello para obter uma lista de pré-requisitos para a tabela a seguir Traga sua própria chave (BYOK) para o Cofre de chaves do Azure.

| Requisito | Mais informações |
| --- | --- |
| Um tooAzure de assinatura |toocreate um cofre de chaves do Azure, você precisa de uma assinatura do Azure: [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) |
| Olá chaves protegidas por HSM do Cofre de chave do Azure Premium serviço camada toosupport |Para obter mais informações sobre as camadas de serviço hello e recursos para o Cofre de chaves do Azure, consulte Olá [preços do Cofre de chaves do Azure](https://azure.microsoft.com/pricing/details/key-vault/) site. |
| HSM da Thales, smartcards e software de suporte |Você deve ter acesso tooa Thales Hardware Security Module e conhecimento operacional básico dos HSMs da Thales. Consulte [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) para lista de saudação de modelos compatíveis ou toopurchase um HSM, se você não tiver um. |
| Olá hardware e software a seguir:<ol><li>Uma estação de trabalho x64 offline com, no mínimo, um sistema operacional Windows 7 e software Thales nShield, versão 11.50 ou posterior.<br/><br/>Se essa estação de trabalho executa o Windows 7, você deve [instalar o Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Uma estação de trabalho que é toohello conectado à Internet e tem um sistema de operacional Windows mínimo do Windows 7 e [Azure PowerShell](/powershell/azure/overview) **versão mínima 1.1.0** instalado.</li><li>Uma unidade USB ou outro dispositivo de armazenamento portátil que tenha pelo menos 16 MB de espaço livre.</li></ol> |Por motivos de segurança, recomendamos que Olá primeira estação de trabalho não está conectado tooa rede. No entanto, essa recomendação não é programaticamente aplicada.<br/><br/>Observe que nas instruções de saudação que seguem, essa estação de trabalho é estação de trabalho chamado tooas Olá desconectado.</p></blockquote><br/>Além disso, se a chave de locatário for para uma rede de produção, recomendamos que você use uma estação de trabalho separada e segundo toodownload Olá conjunto de ferramentas e carregamento Olá chave de locatário. Mas para fins de teste, você pode usar Olá mesma estação de trabalho como Olá primeiro.<br/><br/>Observe que nas instruções de saudação que seguem, essa segunda estação de trabalho é chamado tooas Olá estação de trabalho conectada à Internet.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Gerar e transferir sua chave tooAzure HSM do Cofre de chaves
Você usará Olá toogenerate de cinco etapas a seguir e transferir sua chave tooan HSM do Cofre de chaves do Azure:

* [Etapa 1: preparar sua estação de trabalho conectada à Internet](#step-1-prepare-your-internet-connected-workstation)
* [Etapa 2: preparar sua estação de trabalho desconectada](#step-2-prepare-your-disconnected-workstation)
* [Etapa 3: Gerar a sua chave](#step-3-generate-your-key)
* [Etapa 4: Preparar a sua chave para transferência](#step-4-prepare-your-key-for-transfer)
* [Etapa 5: Transferir sua chave tooAzure Cofre de chaves](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Etapa 1: preparar sua estação de trabalho conectada à Internet
Para a primeira etapa, Olá procedimentos a seguir em sua estação de trabalho é toohello conectado à Internet.

### <a name="step-11-install-azure-powershell"></a>Etapa 1.1: Instalar o Azure PowerShell
De saudação conectada à Internet estação de trabalho, baixe e instale o módulo do PowerShell do Azure Olá que inclui Olá cmdlets toomanage Cofre de chaves do Azure. Isso requer uma versão mínima do 0.8.13.

Para obter instruções de instalação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Etapa 1.2: Obter a sua ID da assinatura do Azure
Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure usando o comando a seguir de saudação:

        Add-AzureAccount
Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha. Em seguida, use Olá [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:

        Get-AzureSubscription
Da saída de hello, localize a ID de Olá para assinatura Olá que você usará para o Cofre de chaves do Azure. Você precisará dessa ID da assinatura mais tarde.

Não feche a janela do PowerShell do Azure hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Etapa 1.3: Baixar Olá conjunto de ferramentas BYOK para Cofre de chaves do Azure
Vá toohello Microsoft Download Center e [baixar o conjunto de ferramentas do BYOK do Cofre de chaves do Azure Olá](http://www.microsoft.com/download/details.aspx?id=45345) para sua região ou instância do Azure. Use os seguintes Olá toodownload de nome de pacote do informações tooidentify hello e seu correspondente SHA-256 hash do pacote:

- - -
**Estados Unidos:**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europa:**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Ásia:**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**América Latina:**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japão:**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Coreia:**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Austrália:**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**US Government DoD:**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Canadá:**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Alemanha:**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**Índia:**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Reino Unido:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

integridade de saudação toovalidate de seu download conjunto de ferramentas BYOK, de sua sessão do PowerShell do Azure, use Olá [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

conjunto de ferramentas de saudação inclui o seguinte hello:

* Um pacote de Chave de Troca de Chave (KEK) que tem um nome que começa com **BYOK-KEK-pkg-.**
* Um pacote de Universo de Segurança que tem um nome que começa com **BYOK-SecurityWorld-pkg-.**
* Um script do Python chamado **verifykeypackage.py.**
* Um arquivo executável de linha de comando chamado **KeyTransferRemote.exe** e DLLs associadas.
* Um pacote redistribuível do Visual C++, chamado **vcredist_x64.exe.**

Copie a unidade do hello pacote tooa USB ou outro armazenamento portátil.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Etapa 2: preparar sua estação de trabalho desconectada
Para essa segunda etapa, Olá seguindo os procedimentos na estação de trabalho de saudação que não está conectado tooa rede (Olá Internet ou sua rede interna).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Etapa 2.1: Preparar Olá desconectado de estação de trabalho com HSM da Thales
Instalar o software de suporte nCipher (Thales) hello em um computador Windows e anexe um computador de toothat HSM da Thales.

Certifique-se de que Olá ferramentas Thales estão no caminho (**%nfast_home%\bin**). Por exemplo, digite o seguinte hello:

        set PATH=%PATH%;"%nfast_home%\bin"

Para obter mais informações, consulte o guia do usuário de saudação incluído com hello HSM da Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Etapa 2.2: Conjunto de ferramentas Install Olá BYOK na estação de trabalho Olá desconectado
Copie o pacote de conjunto de ferramentas do BYOK de saudação da unidade do hello USB ou outro armazenamento portátil e, em seguida, Olá a seguir:

1. Extrai arquivos de saudação do pacote de saudação baixada em qualquer pasta.
2. Nessa pasta, execute o vcredist_x64.exe.
3. Siga as instruções de saudação toohello instalar componentes de tempo de execução do Visual C++ Olá para Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Etapa 3: Gerar a sua chave
Para a terceira etapa, Olá procedimentos a seguir na estação de trabalho Olá desconectado. toocomplete essa etapa de seu HSM deve estar no modo de inicialização. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Etapa 3.1: Alterar Olá HSM modo too'I'
Se você estiver usando Thales nShield borda, modo de saudação toochange: 1. Use Olá modo botão toohighlight Olá modo necessário. 2. Em alguns segundos, pressione e segure o botão Limpar Olá para alguns segundos. Se o modo de saudação for alterado, Olá novo modo para de LED piscando e permanece aceso. Olá LED de Status pode flash irregular por alguns segundos e, em seguida, pisca regularmente quando o dispositivo hello está pronto. Caso contrário, a saudação dispositivo permanece no modo atual hello, com o modo apropriado de saudação LED aceso.

### <a name="step-32-create-a-security-world"></a>Etapa 3.2: Criar um universo de segurança
Inicie um prompt de comando e execute Olá programa do novo mundo Thales.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Este programa cria um **mundo de segurança** arquivo % NFAST_KMDATA%\local\world, que corresponde a toohello C:\ProgramData\nCipher\Key Management Data\local pasta. Você pode usar valores diferentes para quorum hello, mas no nosso exemplo, você está tooenter solicitadas três cartões e em branco pins para cada um. Em seguida, os dois cartões oferecem mundo de segurança toohello acesso completo. Esses cartões se tornam Olá **conjunto de cartões de administrador** para Olá mundo de segurança novo.

Em seguida, Olá a seguir:

* Fazer backup de arquivo do hello world. Proteger e proteger o arquivo do Olá mundo, Olá cartões de administrador e seus pins e certifique-se de que ninguém tenha acesso toomore que um cartão.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Etapa 3.3: Alterar Olá HSM modo too'O'
Se você estiver usando Thales nShield borda, modo de saudação toochange: 1. Use Olá modo botão toohighlight Olá modo necessário. 2. Em alguns segundos, pressione e segure o botão Limpar Olá para alguns segundos. Se o modo de saudação for alterado, Olá novo modo para de LED piscando e permanece aceso. Olá LED de Status pode flash irregular por alguns segundos e, em seguida, pisca regularmente quando o dispositivo hello está pronto. Caso contrário, a saudação dispositivo permanece no modo atual hello, com o modo apropriado de saudação LED aceso.


### <a name="step-34-validate-hello-downloaded-package"></a>Etapa 3.4: Validar o pacote de saudação baixada
Esta etapa é opcional mas recomendado para que você possa validar a seguir hello:

* Olá chave de troca de chave que está incluído no conjunto de ferramentas Olá foi gerada de um Thales HSM genuíno.
* hash de saudação do Olá mundo de segurança que está incluído no conjunto de ferramentas Olá foi gerada em um Thales HSM genuíno.
* Olá Key Exchange Key é não exportável.

> [!NOTE]
> Olá toovalidate baixado o pacote, hello HSM deve estar conectado, ligado e deve ter um mundo de segurança nele (como Olá um que você acabou de criar).
>
>

pacote de saudação baixada toovalidate:

1. Execute Olá script verifykeypackage.py digitando uma das seguintes hello, dependendo da sua região ou instância do Azure:

   * Para a América do Norte:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Para a Europa:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Para a Ásia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Para a América Latina:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Para o Japão:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Para a Coreia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Para a Austrália:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Para US Government DoD:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Para o Canadá:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Para a Alemanha:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Para a Índia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Olá software Thales inclui python em %NFAST_HOME%\python\bin
     >
     >
2. Confirme que você vê Olá seguinte, que indica a validação bem-sucedida: **resultado: êxito**

Este script valida a cadeia do assinante Olá backup toohello chave raiz Thales. Olá hash dessa chave raiz está inserido no script hello e seu valor deve ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Você também pode confirmar esse valor separadamente visitando Olá [site da Thales](http://www.thalesesec.com/).

Agora você está pronto toocreate uma nova chave.

### <a name="step-35-create-a-new-key"></a>Etapa 3.5: Criar uma nova chave
Gerar uma chave usando Olá Thales **generatekey** programa.

Execute Olá chave de saudação do toogenerate de comando a seguir:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Quando você executar esse comando, use estas instruções:

* Olá parâmetro *proteger* deve ser definido como o valor de toohello **módulo**, conforme mostrado. Isso cria uma chave protegida pelo módulo. Olá conjunto de ferramentas BYOK não dá suporte a chaves protegidas por OCS.
* Substituir valor de saudação do *contosokey* para Olá **ident** e **plainname** com qualquer valor de cadeia de caracteres. custos administrativos toominimize e reduzir o risco de saudação de erros, recomendamos que você use Olá mesmo valor para ambos. Olá **ident** valor deve conter somente números, traços, letras maiusculas e minúsculas.
* Olá pubexp é deixado em branco (padrão) neste exemplo, mas você pode especificar valores específicos. Para obter mais informações, consulte Olá documentação da Thales.

Este comando cria um arquivo de chave de token na pasta %NFAST_KMDATA%\local com um nome iniciado por **key_simple _**, seguido pelo Olá **ident** que foi especificado no comando hello. Por exemplo: **key_simple_contosokey**. Esse arquivo contém uma chave criptografada.

Faça backup deste arquivo de Chave com Token em um local seguro.

> [!IMPORTANT]
> Quando você transfere sua chave tooAzure Cofre de chaves posteriormente, o Microsoft não poderá exportar esta chave tooyou back por é extremamente importante que você faça backup do seu mundo de segurança e de chave com segurança. Entre em contato com a Thales para obter orientação e as práticas recomendadas para fazer backup da sua chave.
>
>

Você é agora pronto tootransfer sua chave tooAzure Cofre de chaves.

## <a name="step-4-prepare-your-key-for-transfer"></a>Etapa 4: Preparar a sua chave para transferência
Para esta etapa quarta, Olá procedimentos a seguir na estação de trabalho Olá desconectado.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Etapa 4.1: Criar uma cópia da chave com permissões reduzidas

Abra um prompt de comando novo e alterar Olá atual toohello local do diretório onde você descompactou o arquivo zip do hello BYOK. permissões de saudação tooreduce em sua chave, em um prompt de comando, execute um dos seguintes hello, dependendo da sua região ou instância do Azure:

* Para a América do Norte:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Para a Europa:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Para a Ásia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Para a América Latina:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Para o Japão:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Para a Coreia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Para a Austrália:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Para US Government DoD:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Para o Canadá:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Para a Alemanha:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Para a Índia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Quando você executa esse comando, substitua *contosokey* com hello mesmo valor especificado em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.

Você será solicitado a tooplug seus cartões de administrador do mundo de segurança.

Quando Olá comando for concluído, você verá **resultado: êxito** e cópia de saudação da sua chave com permissões reduzidas são no arquivo hello chamado key_xferacid _<contosokey>.

Pode inspeciona Olá ACLS usando o seguinte comandos usando Olá utilitários Thales:

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Quando você executar esses comandos, substitua contosokey Olá mesmo valor especificado em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Etapa 4.2: Criptografar a chave usando a Chave de Troca de Chaves da Microsoft
Execute um dos Olá comandos, dependendo da sua região ou instância do Azure a seguir:

* Para a América do Norte:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Europa:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Ásia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a América Latina:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para o Japão:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Coreia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Austrália:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa a instância do governo Olá dos EUA do Azure:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para US Government DoD:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para o Canadá:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Alemanha:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para a Índia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Quando você executar esse comando, use estas instruções:

* Substituir *contosokey* com identificador de saudação que é usado como chave de saudação toogenerate em **3.5 etapa: criar uma nova chave** de saudação [gerar sua chave](#step-3-generate-your-key) etapa.
* Substituir *SubscriptionID* com ID Olá Olá assinatura do Azure que contém seu Cofre de chaves. Esse valor foi recuperado anteriormente, em **etapa 1.2: Obtenha sua ID de assinatura do Azure** de saudação [preparar sua estação de trabalho conectada à Internet](#step-1-prepare-your-internet-connected-workstation) etapa.
* Substitua *ContosoFirstHSMKey* por um rótulo que seja usado para o nome do arquivo de saída.

Quando isso for concluído com êxito, ele exibe **resultado: êxito** e há um novo arquivo na pasta atual Olá tem Olá nome a seguir: KeyTransferPackage -*ContosoFirstHSMkey*. byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Etapa 4.3: Copiar a transferência de chave pacote toohello conectada à Internet estação de trabalho
Use uma unidade USB ou outro arquivo de saída do armazenamento portátil toocopy Olá de saudação anterior (KeyTransferPackage-ContosoFirstHSMkey.byok) da etapa tooyour conectada à Internet estação de trabalho.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Etapa 5: Transferir sua chave tooAzure Cofre de chaves
Para essa etapa final, Olá conectada à Internet estação de trabalho, use Olá [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload Olá chave pacote de transferência que você copiou da saudação desconectado toohello de estação de trabalho HSM do Cofre de chaves do Azure:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Se Olá upload for bem-sucedido, você verá propriedades Olá exibido da chave de saudação que você acabou de adicionar.

## <a name="next-steps"></a>Próximas etapas
Agora você pode usar essa chave de HSM protegido no Cofre da Chave. Para obter mais informações, consulte Olá **se você quiser que um módulo de segurança de hardware (HSM) de toouse** seção Olá [guia de Introdução ao Azure Key Vault](key-vault-get-started.md) tutorial.
