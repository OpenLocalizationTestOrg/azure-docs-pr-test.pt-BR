---
title: aaaHow toouse armazenamento de Blob do Xamarin | Microsoft Docs
description: "Olá biblioteca de cliente de armazenamento do Azure para Xamarin permite que os desenvolvedores toocreate iOS, Android e aplicativos da Windows Store com suas interfaces de usuário nativo. Este tutorial mostra como toouse Xamarin toocreate um aplicativo que usa o armazenamento de BLOBs do Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Como toouse armazenamento de Blob do Xamarin
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Visão geral
Xamarin permite que os desenvolvedores toouse compartilhado c# codebase toocreate iOS, Android e aplicativos da Windows Store com suas interfaces de usuário nativo. Este tutorial mostra como toouse armazenamento de BLOBs do Azure com um aplicativo Xamarin. Se você quiser toolearn mais sobre o armazenamento do Azure, antes de mergulhar no código hello, consulte [tooMicrosoft Introdução armazenamento do Azure](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Criar um novo aplicativo Xamarin
Neste tutorial, criaremos um aplicativo para Android, iOS e Windows. Este aplicativo simplesmente criará um contêiner e carregará um blob nesse contêiner. Usaremos o Visual Studio no Windows, mas Olá conhecimentos mesmo podem ser aplicados durante a criação de um aplicativo usando o Xamarin Studio macOS.

Siga estas etapas toocreate seu aplicativo:

1. Se você ainda não o fez, baixe e instale o [Xamarin para Visual Studio](https://www.xamarin.com/download).
2. Abra o Visual Studio e crie um Aplicativo em Branco (Portátil nativo): **Arquivo > Novo > Projeto > Plataforma Cruzada > Aplicativo em Branco (Portátil nativo)**.
3. Clique em sua solução no painel do Gerenciador de soluções hello e selecione **gerenciar pacotes NuGet para solução**. Procurar **windowsazure** e instalar os projetos de tooall versão estável mais recentes Olá em sua solução.
4. Compile e execute seu projeto.

Agora você deve ter um aplicativo que permite que você tooclick um botão que incrementa um contador.

## <a name="create-container-and-upload-blob"></a>Criar contêiner e carregar blob
Em seguida, em seu `(Portable)` projeto, você adicionará um código muito`MyClass.cs`. Esse código cria um contêiner e carrega um blob nesse contêiner. `MyClass.cs`deve ter aparência Olá a seguir:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Certifique-se de que tooreplace "your_account_name_here" e "your_account_key_here" com o nome da conta real e a chave de conta. 

O iOS, Android e Windows Phone projetos todos têm referências tooyour projeto portátil - que significa que você pode escrever todo o código compartilhado em um colocam e usá-lo em todos os seus projetos. Agora você pode adicionar Olá a seguinte linha de código tooeach projeto toostart aproveitando:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Executar o aplicativo hello
Agora você pode executar esse aplicativo em um emulador do Android ou do Windows Phone. Também é possível executar esse aplicativo em um emulador de iOS, mas isso exigirá um Mac. Para obter instruções específicas sobre como toodo isso, leia a documentação Olá para [conectar-se o Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Quando você executa seu aplicativo, ele criará o contêiner Olá `mycontainer` na sua conta de armazenamento. Ela deve conter o blob hello, `myblob`, que tem o texto de saudação `Hello, world!`. Você pode verificar isso usando Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate um aplicativo de plataforma cruzada no Xamarin que usa armazenamento do Azure, concentrando-se especificamente um cenário no armazenamento de Blob. No entanto, você pode fazer muito mais, não apenas com o Armazenamento de Blobs, mas também com o Armazenamento de Filas, de Tabelas e de Arquivo. Faça check-out Olá artigos toolearn mais a seguir:

* [Introdução ao armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md)
* [Introdução ao armazenamento de Tabelas do Azure usando o .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introdução ao armazenamento de Fila do Azure usando o .NET](../queues/storage-dotnet-how-to-use-queues.md)
* [Introdução ao Armazenamento de Arquivos do Azure no Windows](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

