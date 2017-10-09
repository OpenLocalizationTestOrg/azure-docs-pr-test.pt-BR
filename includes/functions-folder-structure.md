
código de saudação para todas as funções hello em um aplicativo de determinada função reside em uma pasta raiz que contém um arquivo de configuração do host e as subpastas de um ou mais, cada qual contendo código Olá para uma função separada, como no exemplo a seguir de saudação:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Olá *host.json* arquivo contém algumas configurações específicas de tempo de execução e se encontra na pasta raiz de saudação do aplicativo de função hello. Para obter informações sobre as configurações que estão disponíveis, consulte [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) no wiki do hello WebJobs.Script repositório.

Cada função tem uma pasta que contém um ou mais arquivos de código, configuração de function.json hello e outras dependências.

