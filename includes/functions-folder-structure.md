
<span data-ttu-id="ee0d5-101">código de saudação para todas as funções hello em um aplicativo de determinada função reside em uma pasta raiz que contém um arquivo de configuração do host e as subpastas de um ou mais, cada qual contendo código Olá para uma função separada, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="ee0d5-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="ee0d5-102">Olá *host.json* arquivo contém algumas configurações específicas de tempo de execução e se encontra na pasta raiz de saudação do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="ee0d5-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="ee0d5-103">Para obter informações sobre as configurações que estão disponíveis, consulte [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) no wiki do hello WebJobs.Script repositório.</span><span class="sxs-lookup"><span data-stu-id="ee0d5-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="ee0d5-104">Cada função tem uma pasta que contém um ou mais arquivos de código, configuração de function.json hello e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="ee0d5-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

