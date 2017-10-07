---
title: "aaaCryptography - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Estrutura de segurança: Criptografia | Atenuações 
| Produto/serviço | Artigo |
| --------------- | ------- |
| **Aplicativo Web** | <ul><li>[Usar somente codificações de bloco simétricas e comprimentos de chave aprovados](#cipher-length)</li><li>[Usar modos de codificação de bloco aprovados e vetores de inicialização para codificações simétricas](#vector-ciphers)</li><li>[Usar algoritmos assimétricos, comprimentos de chave e preenchimentos aprovados](#padding)</li><li>[Usar um número aleatório de geradores aprovados](#numgen)</li><li>[Não usar codificações de fluxo simétricas](#stream-ciphers)</li><li>[Usar algoritmos MAC, HMAC e de hash com chave](#mac-hash)</li><li>[Usar apenas as funções aprovadas do hash criptográfico](#hash-functions)</li></ul> |
| **Banco de dados** | <ul><li>[Usar dados de tooencrypt de algoritmos de criptografia forte no banco de dados de saudação](#strong-db)</li><li>[Os pacotes do SSIS devem ser criptografados e assinados digitalmente](#ssis-signed)</li><li>[Adicionar assinatura digital protegíveis de banco de dados de toocritical](#securables-db)</li><li>[Usar chaves de criptografia do SQL server EKM tooprotect](#ekm-keys)</li><li>[Use o recurso de AlwaysEncrypted se as chaves de criptografia não devem ser reveladas tooDatabase mecanismo](#keys-engine)</li></ul> |
| **Dispositivo IoT** | <ul><li>[Armazenar chaves de criptografia com segurança no dispositivo IoT](#keys-iot)</li></ul> | 
| **Gateway de Nuvem IoT** | <ul><li>[Gerar uma chave simétrica aleatória de tamanho suficiente para autenticação tooIoT Hub](#random-hub)</li></ul> | 
| **Cliente móvel do Dynamics CRM** | <ul><li>[Garantir que uma política de gerenciamento de dispositivos esteja aplicada, que ela exija um PIN de uso e permita a limpeza remota do dispositivo](#pin-remote)</li></ul> | 
| **Cliente do Outlook do Dynamics CRM** | <ul><li>[Garantir que uma política de gerenciamento de dispositivos esteja aplicada, que exija PIN, senha ou bloqueio automático e criptografe todos os dados (por exemplo, o BitLocker)](#bitlocker)</li></ul> | 
| **Identity Server** | <ul><li>[Garantir que as chaves de assinatura sejam trocadas quando o Servidor de identidade for usado](#rolled-server)</li><li>[Garantir que ID de cliente e segredo do cliente criptograficamente fortes sejam usados no Identity Server](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Usar somente codificações de bloco simétricas e comprimentos de chave aprovados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Produtos devem usar somente essas codificações em bloco simétrica e comprimentos de chave associados que foram aprovados explicitamente pelo Olá Supervisor de criptografia em sua organização. Algoritmos simétricos aprovados na Microsoft incluem hello codificações em bloco a seguir:</p><ul><li>Para um novo código, AES-128, AES 192 e AES-256 são aceitáveis.</li><li>Para garantir a compatibilidade com versões anteriores do código existente, a chave tripla 3DES é aceitável.</li><li>Para os produtos que usam codificações de bloco simétricas:<ul><li>A criptografia AES (Advanced Encryption Standard) é necessária para novos códigos.</li><li>O padrão de criptografia 3DES (Triple Data Encryption Standard) com três chaves é permitido em códigos existentes e para garantir a compatibilidade com versões anteriores.</li><li>Todas as outras codificações de bloco, incluindo RC2, DES, 3DES com duas chaves, DESX e Skipjack, só podem ser usadas para descriptografar os dados antigos e devem ser substituídas se utilizadas para criptografia.</li></ul></li><li>Para algoritmos de criptografia de bloco simétrica, é preciso ter um comprimento mínimo de chave de 128 bits. Olá, somente o algoritmo de criptografia de bloco recomendado para novo código é AES (AES-128, AES 192 e AES-256 são todos aceitável)</li><li>Três chave 3DES é atualmente aceitável se já está em uso no código existente. é recomendável tooAES de transição. Os algoritmos DESX, DES, RC2 e Skipjack não são mais considerados seguros. Esses algoritmos só podem ser usados para descriptografar os dados existentes para a mesma Olá de compatibilidade com versões anteriores e dados devem ser criptografados novamente usando uma codificação de bloco recomendado</li></ul><p>Observe que todas as codificações de bloco simétricas devem ser usadas com um modo de codificação aprovado, que exige o uso de um vetor de inicialização (IV) apropriado. Normalmente, um IV apropriado é um número aleatório e nunca um valor constante.</p><p>uso de saudação de algoritmos de criptografia não aprovados herdados ou de outra forma e comprimentos de chave menores para a leitura de dados existentes (como toowriting contrário novos dados) pode ser permitido após revisar do quadro de criptografia da sua organização. No entanto, você deve solicitar uma exceção para esse requisito. Além disso, em implantações corporativas, produtos devem considerar os administradores de aviso quando criptografia fraca dados tooread usado. Esses avisos devem ser explicativos e acionáveis. Em alguns casos, pode ser apropriado toohave política de grupo Olá utiliza de criptografia fraca</p><p>Algoritmos do .NET permitidos para agilidade criptográfica gerenciada (em ordem de preferência)</p><ul><li>AesCng (em conformidade com FIPS)</li><li>AuthenticatedAesCng (em conformidade com FIPS)</li><li>AESCryptoServiceProvider (em conformidade com FIPS)</li><li>AESManaged (sem conformidade com FIPS)</li></ul><p>Observe que nenhum desses algoritmos podem ser especificados por meio de saudação `SymmetricAlgorithm.Create` ou `CryptoConfig.CreateFromName` métodos sem fazer o arquivo de Machine. config toohello alterações. Além disso, observe que o AES em versões do too.NET anterior do .NET 3.5 é denominada `RijndaelManaged`, e `AesCng` e `AuthenticatedAesCng` são > disponível por meio do CodePlex e exigem CNG em Olá subjacente do sistema operacional</p>

## <a id="vector-ciphers"></a>Usar modos de codificação de bloco aprovados e vetores de inicialização para codificações simétricas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Todas as codificações de bloco simétricas devem ser usadas com um modo de decodificação simétrica aprovado. modos de Olá somente aprovado são CBC e CTS. Em particular, o modo de operação de saudação código eletrônico catálogo (ECB) deve ser evitado; uso de ECB requer a revisão de placa de criptografia da sua organização. Todos os usos de OFB, CFB, CTR, CCM e GCM, ou de qualquer outro modo de criptografia, devem revisados pelos especialistas em criptografia de sua organização. Reutilizando Olá mesmo vetor de inicialização (IV) com codificações em bloco em "streaming codificações modos," como CTR, pode fazer com que os dados criptografados toobe revelada. Todas as codificações de bloco simétricas também devem ser usadas com IV apropriado, que é um número aleatório criptograficamente forte e nunca um valor constante. |

## <a id="padding"></a>Usar algoritmos assimétricos, comprimentos de chave e preenchimentos aprovados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>uso de saudação de algoritmos criptográficos banidos apresenta um risco significativo tooproduct segurança e deve ser evitado. Os produtos devem usar somente os algoritmos de criptografia, os comprimentos de chave associados e o preenchimento que foram explicitamente aprovados pelos especialistas em criptografia de sua organização.</p><ul><li>**RSA -** pode ser usada para assinatura, troca de chaves e criptografia. Criptografia de RSA deve usar apenas Olá OAEP ou RSA KEM preenchimento modos. O código existente pode usar o modo de preenchimento PKCS #1 v 1.5 somente para fins de compatibilidade. O uso do preenchimento nulo é expressamente proibido. É necessário usar chaves com 2048 bits ou mais para um novo código. O código existente pode oferecer suporte a chaves com menos de 2048 bits somente para garantir a compatibilidade com versões anteriores após a revisão dos especialistas em criptografia de sua organização. As chaves com menos de 1024 só podem ser usadas para descriptografar ou verificar dados antigos e devem ser substituídas para operações de criptografia ou assinatura.</li><li>**ECDSA -** pode ser usada somente para assinatura. É necessário o ECDSA com chaves de 256 bits ou mais para um novo código. Assinaturas de ECDSA devem usar uma das curvas do NIST aprovada Olá três (p-256, p-384 ou P521). As curvas que foram minuciosamente analisada poderão ser usadas somente após uma revisão dos especialistas em criptografia de sua organização.</li><li>**ECDH -** pode ser usada somente para troca de chaves. É necessário o ECDH com chaves de 256 bits ou mais para um novo código. Troca de chaves com base em ECDH deve usar uma das curvas do NIST aprovada Olá três (p-256, p-384 ou P521). As curvas que foram minuciosamente analisada poderão ser usadas somente após uma revisão dos especialistas em criptografia de sua organização.</li><li>**DSA -** pode ser aceitável após revisão e aprovação dos especialistas em criptografia de sua organização. Entre em contato com seu tooschedule do Supervisor de segurança revisão de quadro de criptografia da sua organização. Se o uso do DSA for aprovado, observe que você precisará tooprohibit uso de chaves de menos de 2048 bits de comprimento. A CNG oferece suporte a chaves com 2048 bits ou mais a partir do Windows 8.</li><li>**Diffie-Hellman -** pode ser usada somente para o gerenciamento de chaves de sessão. É necessário usar chaves com 2048 bits ou mais para um novo código. O código existente pode dar suporte a chaves com menos de 2048 bits somente para garantir a compatibilidade com versões anteriores, após um exame do Conselho de criptografia de sua organização. Chaves com menos de 1024 bits não podem ser usadas.</li><ul>

## <a id="numgen"></a>Usar um número aleatório de geradores aprovados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Os produtos devem usar um número aleatório de geradores aprovados. Números pseudoaleatórios funções como rand de função do tempo de execução Olá C, classe do .NET Framework Olá Random ou funções do sistema como ObterContagemMarcaEscala devem, portanto, nunca ser usadas em tal código. É proibido o uso de saudação dupla curva elíptica aleatório algoritmo gerador de números (DUAL_EC_DRBG)</p><ul><li>**CNG -** BCryptGenRandom (uso do sinalizador BCRYPT_USE_SYSTEM_PREFERRED_RNG de saudação recomendada a menos que o chamador Olá pode ser executado em qualquer IRQL maior que 0 [ou seja, PASSIVE_LEVEL])</li><li>**CAPI-** cryptGenRandom</li><li>**Win32/64-** RtlGenRandom (as novas implementações devem usar BCryptGenRandom ou CryptGenRandom) * rand_s * SystemPrng (para o modo kernel)</li><li>**.NET-** RNGCryptoServiceProvider ou RNGCng</li><li>**Aplicativos da Windows Store-** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom ou .GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef aleatório, size_t contagem, uint8_t *bytes)</li><li>**Apple OS X (< 10.7)-** Use / números aleatórios tooretrieve dev/aleatória</li><li>**Java(including Google Android Java Code) –** java.security.SecureRandom class. Observe que para Android 4.3 (Jelly Bean), os desenvolvedores devem seguir Olá Android recomendado para solucionar esse problema e atualizar seu aplicativos tooexplicitly inicializar Olá PRNG com entropia de /dev/urandom ou /dev/random</li></ul>|

## <a id="stream-ciphers"></a>Não usar codificações de fluxo simétricas

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Codificações de stream simétricas, como RC4, não devem ser usadas. Em vez de codificações de stream simétricas, os produtos devem usar uma codificação de bloco, especificamente a AES com uma chave de pelo menos 128 bits. |

## <a id="mac-hash"></a>Usar algoritmos MAC, HMAC e de hash com chave

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Os produtos devem usar somente algoritmos de código de autenticação de mensagem (MAC) ou de código de autenticação de mensagem baseada em hash (HMAC) aprovados.</p><p>Um código de autenticação de mensagem (MAC) é uma parte da mensagem de tooa anexado informações que permite que seu destinatário tooverify tanto autenticidade de saudação do remetente hello e integridade de saudação de mensagem de saudação usando uma chave secreta. Olá o uso de qualquer um MAC baseadas em hash ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) ou [com base em codificação de bloco MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) é permitido como algoritmos de criptografia simétrica ou hash de todas as subjacente também são aprovados para uso; atualmente isso inclui Olá funções de SHA2 HMAC (HMAC-SHA256, SHA384 HMAC e HMAC-SHA512) e hello CMAC/OMAC1 e OMAC2 bloqueiam MACs baseados em criptografia (eles se baseiam em AES).</p><p>Uso de HMAC-SHA1 pode ser permitido para compatibilidade de plataforma, mas que será necessário toofile um procedimento de toothis de exceção e passar por uma revisão de criptografia da sua organização. Não é permitido truncar HMACs tooless de 128 bits. Usar métodos de cliente toohash uma chave e os dados não foi aprovada e deve passar por toouse anterior do revisão da sua organização quadro de criptografia.</p>|

## <a id="hash-functions"></a>Usar apenas as funções aprovadas do hash criptográfico

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Produtos devem usar a família Olá SHA-2 de algoritmos de hash (SHA256, SHA384 e SHA512). Se for necessário um hash mais curto, como um tamanho de 128 bits de saída em ordem toofit uma estrutura de dados criada com o hash MD5 menor Olá em mente, as equipes do produto podem truncar um hashes de SHA2 hello (normalmente SHA256). Observe que o SHA384 é uma versão truncada do SHA512. Truncamento de hashes criptográficos para tooless de fins de segurança de 128 bits não é permitido. Novo código não deve usar os algoritmos de hash MD2, MD4, MD5, SHA-0, SHA-1 ou RIPEMD hello. É possível realizar colisões de hash computacionalmente para esses algoritmos, o que efetivamente os quebrará.</p><p>Algoritmos de hash do .NET permitidos para agilidade criptográfica gerenciada (em ordem de preferência)</p><ul><li>SHA512Cng (em conformidade com FIPS)</li><li>SHA384Cng (em conformidade com FIPS)</li><li>SHA256Cng (em conformidade com FIPS)</li><li>SHA512Managed (não-compatível com FIPS) (use SHA512 como nome do algoritmo em chamadas tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA384Managed (não-compatível com FIPS) (use SHA384 como o nome do algoritmo em chamadas tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA256Managed (não-compatível com FIPS) (use SHA256 como nome do algoritmo em chamadas tooHashAlgorithm.Create ou CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (em conformidade com FIPS)</li><li>SHA256CryptoServiceProvider (em conformidade com FIPS)</li><li>SHA384CryptoServiceProvider (em conformidade com FIPS)</li></ul>| 

## <a id="strong-db"></a>Usar dados de tooencrypt de algoritmos de criptografia forte no banco de dados de saudação

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Escolhendo um algoritmo de criptografia](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Etapas** | Os algoritmos de criptografia definem as transformações de dados que não podem ser facilmente revertidas por usuários não autorizados. SQL Server permite que os administradores e desenvolvedores toochoose entre diversos algoritmos, incluindo DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, RC4 de 128 bits, DESX, AES de 128 bits, AES de 192 bits e AES de 256 bits |

## <a id="ssis-signed"></a>Os pacotes do SSIS devem ser criptografados e assinados digitalmente

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Identificar Olá origem de pacotes com assinaturas digitais](https://msdn.microsoft.com/library/ms141174.aspx), [de ameaça e mitigação de vulnerabilidade (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Etapas** | origem de saudação do pacote é Olá individual ou a organização que criou o pacote de saudação. Executar um pacote de uma origem desconhecida ou não confiável pode ser arriscado. tooprevent não autorizado a violação de pacotes do SSIS, assinaturas digitais devem ser usadas. Além disso, tooensure confidencialidade de saudação de pacotes de saudação durante o trânsito/armazenamento, pacotes do SSIS têm toobe criptografado |

## <a id="securables-db"></a>Adicionar assinatura digital protegíveis de banco de dados de toocritical

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [ADD SIGNATURE (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **Etapas** | Em casos em que a integridade de um banco de dados crítico protegível Olá tem toobe verificado, assinaturas digitais devem ser usadas. Os protegíveis de um banco de dados, como um procedimento armazenado, uma função, um assembly ou um disparo, podem ser assinados digitalmente. Abaixo está um exemplo de quando isso pode ser útil: digamos um ISV (fornecedor independente de Software) forneceu suporte tooa software distribuído tooone de seus clientes. Antes de fornecer suporte, a saudação ISV desejaria tooensure se um banco de dados podem ser protegido no software de saudação não foi alterado por engano ou por uma tentativa mal-intencionada. Se Olá protegível for assinado digitalmente, Olá ISV pode verificar a assinatura digital e validar sua integridade.| 

## <a id="ekm-keys"></a>Usar chaves de criptografia do SQL server EKM tooprotect

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Gerenciamento extensível de chaves (EKM) do SQL Server](https://msdn.microsoft.com/library/bb895340), [Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Etapas** | Gerenciamento extensível de chaves do SQL Server permite que as chaves de criptografia Olá proteger a saudação toobe de arquivos de banco de dados armazenado em um dispositivo, como um cartão inteligente, o dispositivo USB ou o módulo EKM/HSM. Isso também permite que a proteção de dados dos administradores de banco de dados (exceto os membros do grupo sysadmin de saudação). Dados podem ser criptografados usando chaves de criptografia que apenas hello usuário de banco de dados tem acesso tooon Olá módulo externo de EKM/HSM. |

## <a id="keys-engine"></a>Use o recurso de AlwaysEncrypted se as chaves de criptografia não devem ser reveladas tooDatabase mecanismo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Banco de dados | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | SQL Azure, OnPrem |
| **Atributos**              | Versão do SQL - V12, MsSQL2016 |
| **Referências**              | [Sempre criptografado (mecanismo de banco de dados)](https://msdn.microsoft.com/library/mt163865) |
| **Etapas** | Sempre criptografado é um recurso projetado tooprotect dados confidenciais, como números de cartão de crédito ou de identificação Nacional (por exemplo, números de previdência social), armazenado em bancos de dados do banco de dados SQL ou SQL Server. Sempre criptografado permite que os clientes tooencrypt os dados confidenciais em aplicativos de cliente e nunca revele toohello chaves de criptografia Olá mecanismo de banco de dados (banco de dados SQL ou SQL Server). Como resultado, sempre criptografado fornece uma separação entre aqueles que possuem dados saudação (e podem exibi-lo) e aqueles que gerenciam dados de saudação (mas não devem ter acesso) |

## <a id="keys-iot"></a>Armazenar chaves de criptografia com segurança no dispositivo IoT

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Sistema operacional do dispositivo - Windows IoT Core, Conectividade do dispositivo - SDKs do dispositivo IoT do Azure |
| **Referências**              | [TPM no Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm), [Configurar TPM no Windows IoT Core](https://developer.microsoft.com/windows/iot/win10/setuptpm), [TPM do SDK do dispositivo IoT do Azure](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **Etapas** | Armazene chaves privadas simétricas ou de certificado com segurança em um armazenamento de hardware protegido, um TPM ou chips de cartão inteligente. Windows 10 IoT Core dá suporte a usuário Olá de um TPM e há várias TPMs compatíveis que podem ser usados: https://developer.microsoft.com/windows/iot/win10/tpm. É recomendável toouse um Firmware ou TPM discretos. Um TPM de Software deve ser usado apenas para fins de testes e desenvolvimento. Depois que um TPM está disponível e Olá chaves são provisionadas nele, código de saudação que gera um token de saudação deve ser escrito sem codificação qualquer informação confidencial. | 

### <a name="example"></a>Exemplo
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Como pode ser visto, chave primária do hello dispositivo não está presente no código de saudação. Em vez disso, ele é armazenado no hello TPM no slot 0. Dispositivo TPM gera uma curta duração token SAS que é então usado tooconnect toohello IoT Hub. 

## <a id="random-hub"></a>Gerar uma chave simétrica aleatória de tamanho suficiente para autenticação tooIoT Hub

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Gateway de Nuvem IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | Opção de gateway - Hub IoT do Azure |
| **Referências**              | N/D  |
| **Etapas** | O Hub IoT contém um Registro de Identidade de dispositivo e, ao provisionar um dispositivo, gera automaticamente uma chave simétrica aleatória. É recomendável toouse esse recurso hello Azure IoT Hub identidade toogenerate Olá da chave de registro é usado para autenticação. IoT Hub também permite que uma chave toobe especificado ao criar o dispositivo de saudação. Se uma chave é gerada fora do IoT Hub durante o provisionamento do dispositivo, é recomendável toocreate uma chave simétrica aleatória ou pelo menos de 256 bits. |

## <a id="pin-remote"></a>Garantir que uma política de gerenciamento de dispositivos esteja aplicada, que ela exija um PIN de uso e permita a limpeza remota do dispositivo

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvel do Dynamics CRM | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Garanta que uma política de gerenciamento de dispositivos esteja aplicada, que ela exija um PIN de uso e permita a limpeza remota do dispositivo. |

## <a id="bitlocker"></a>Garantir que uma política de gerenciamento de dispositivos esteja aplicada, que exija PIN, senha ou bloqueio automático e criptografe todos os dados (por exemplo, o BitLocker)

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Cliente do Outlook do Dynamics CRM | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Garanta que uma política de gerenciamento de dispositivos esteja aplicada, que exija PIN, senha ou bloqueio automático e criptografe todos os dados (por exemplo, o BitLocker). |

## <a id="rolled-server"></a>Garantir que as chaves de assinatura sejam trocadas quando o Servidor de identidade for usado

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Implantação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Servidor de identidade - chaves, assinaturas e criptografia](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **Etapas** | Garanta que as chaves de assinatura sejam trocadas quando o Servidor de identidade for usado. Olá link na seção de referências de saudação explica como isso deve ser planejado sem causar interrupções tooapplications confiar no servidor de identidade. |

## <a id="client-server"></a>Garantir que ID de cliente e segredo do cliente criptograficamente fortes sejam usados no Identity Server

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | <p>Garantir que ID de cliente e segredo do cliente criptograficamente fortes sejam usados no Identity Server. Olá diretrizes a seguir deve ser usada ao gerar uma ID de cliente e o segredo:</p><ul><li>Gerar um GUID aleatório Olá a ID de cliente</li><li>Gerar uma chave de 256 bits aleatória criptograficamente como segredo Olá</li></ul>|
