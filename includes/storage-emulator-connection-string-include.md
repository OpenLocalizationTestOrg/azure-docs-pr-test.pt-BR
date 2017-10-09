emulador de armazenamento Olá dá suporte a uma única conta fixa e uma chave de autenticação conhecida para autenticação de chave compartilhada. A conta e a chave são credenciais de chave compartilhada somente Olá permitidas para uso com o emulador de armazenamento hello. Eles são:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> chave de autenticação Olá suportada pelo emulador de armazenamento Olá destina-se somente para teste funcionalidade de saudação do seu código de autenticação de cliente. Ela não serve para fins de segurança. Você não pode usar a conta de armazenamento de produção e a chave com o emulador de armazenamento hello. Você não deve usar a conta de saudação de desenvolvimento com dados de produção.
> 
> emulador de armazenamento Olá dá suporte à conexão via HTTP. No entanto, o HTTPS é recomendado de protocolo para acessar recursos em uma conta de armazenamento do Azure de produção de hello.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Conecte-se a conta do emulador toohello usando um atalho
Olá mais fácil maneira tooconnect toohello emulador de armazenamento de seu aplicativo é tooconfigure uma cadeia de caracteres de conexão no arquivo de configuração do aplicativo que referencia o atalho Olá `UseDevelopmentStorage=true`. Aqui está um exemplo de um emulador de armazenamento de toohello da cadeia de caracteres de conexão em um *App. config* arquivo: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Conecte-se toohello conta do emulador usando a chave e nome de conta bem conhecida Olá
toocreate uma cadeia de caracteres de conexão que referências Olá nome de conta do emulador e chave, você deve especificar pontos de extremidade Olá para cada Olá serviços que você deseja toouse do emulador Olá na cadeia de caracteres de conexão de saudação. Isso é necessário para que a cadeia de caracteres de conexão Olá fará referência Olá emulador pontos de extremidade, que são diferentes para uma conta de armazenamento de produção. Por exemplo, valor de saudação de sua cadeia de caracteres de conexão será assim:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Esse valor é idêntico toohello atalho mostrado acima, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Especificar um proxy HTTP
Quando você estiver testando o seu serviço no emulador de armazenamento hello, você também pode especificar um toouse de proxy HTTP. Isso pode ser útil para observar solicitações e respostas HTTP enquanto você estiver depurando operações em serviços de armazenamento de saudação. toospecify um proxy, adicionar Olá `DevelopmentStorageProxyUri` opção de cadeia de caracteres de conexão toohello e defina o URI de proxy toohello seu valor. Por exemplo, aqui está uma cadeia de caracteres de conexão que aponta o emulador de armazenamento toohello e configura um proxy HTTP:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

