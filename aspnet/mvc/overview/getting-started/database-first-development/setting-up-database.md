---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: Introdução ao Entity Framework 6 Database First usando MVC 5 | Microsoft Docs
author: tfitzmac
description: Usando o MVC, Entity Framework e o Scaffolding do ASP.NET, você pode criar um aplicativo web que fornece uma interface para um banco de dados existente. Esta série de tutoriais...
ms.author: aspnetcontent
ms.date: 10/01/2014
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: 20e590ad1b3a59f93d1ba48a2564ddc1a5cbb315
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836114"
---
<a name="getting-started-with-entity-framework-6-database-first-using-mvc-5"></a>Introdução ao Entity Framework 6 Database First usando MVC 5
====================
por [Tom FitzMacken](https://github.com/tfitzmac)

> Usando o MVC, Entity Framework e o Scaffolding do ASP.NET, você pode criar um aplicativo web que fornece uma interface para um banco de dados existente. Esta série de tutoriais mostra como automaticamente gerar um código que permite aos usuários exibir, editar, criar e excluir dados que residem em uma tabela de banco de dados. O código gerado corresponde às colunas na tabela de banco de dados. A última parte da série, você implantará o site e o banco de dados no Azure.
> 
> Esta parte da série se concentra na criação de um banco de dados e populá-lo com dados.
> 
> Esta série foi gravada com contribuições de Tom Dykstra e Rick Anderson. Ele foi aprimorado com base nos comentários dos usuários na seção de comentários.


## <a name="introduction"></a>Introdução

Este tópico mostra como começar com um existente de banco de dados e criar rapidamente um aplicativo web que permite aos usuários interagir com os dados. Ele usa o Entity Framework 6 e ao MVC 5 para compilar o aplicativo web. O recurso de Scaffolding do ASP.NET permite que você gerar automaticamente o código para exibir, atualizar, criar e excluir dados. Usando as ferramentas de publicação no Visual Studio, você pode facilmente implantar o site e o banco de dados no Azure.

Este tópico aborda a situação em que você tenha um banco de dados e deseja gerar código para um aplicativo web com base nos campos do banco de dados. Essa abordagem é chamada de desenvolvimento de banco de dados primeiro. Se você ainda não tiver um banco de dados existente, você pode usar uma abordagem denominada desenvolvimento Code First que envolve a definição de classes de dados e gerar o banco de dados das propriedades de classe.

Para obter um exemplo introdutório de desenvolvimento Code First, consulte [Introdução ao ASP.NET MVC 5](../introduction/getting-started.md). Para obter um exemplo mais avançado, consulte [criando um modelo de dados do Entity Framework para um aplicativo do ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

Para obter orientação sobre como selecionar qual abordagem do Entity Framework para usar, consulte [abordagens de desenvolvimento do Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).

## <a name="prerequisites"></a>Pré-requisitos

Visual Studio 2013 ou Visual Studio Express 2013 para Web

## <a name="set-up-the-database"></a>Configurar o banco de dados

Para imitar o ambiente de ter um banco de dados existente, você primeiro crie um banco de dados com alguns dados previamente preenchidos e, em seguida, crie seu aplicativo web que se conecta ao banco de dados.

Este tutorial foi desenvolvido usando LocalDB com o Visual Studio 2013 ou Visual Studio Express 2013 para Web. Você pode usar um servidor de banco de dados existente em vez do LocalDB, mas dependendo da sua versão do Visual Studio e seu tipo de banco de dados, todas as ferramentas de dados no Visual Studio não podem ter suporte. Se as ferramentas não estão disponíveis para seu banco de dados, você precisa executar algumas etapas específicas do banco de dados dentro do pacote de gerenciamento do banco de dados.

Se você tiver um problema com as ferramentas de banco de dados na sua versão do Visual Studio, verifique se que você instalou a versão mais recente das ferramentas de banco de dados. Para obter informações sobre como atualizar ou instalar as ferramentas de banco de dados, consulte [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).

Inicie o Visual Studio e crie uma **projeto de banco de dados do SQL Server**. Nomeie o projeto **ContosoUniversityData**.

![Criar projeto de banco de dados](setting-up-database/_static/image1.png)

Agora você tem um projeto de banco de dados vazio. Você implantará este banco de dados para o Azure posteriormente no tutorial, portanto, você precisará definir o banco de dados SQL como a plataforma de destino para o projeto. Definir a plataforma de destino não realmente implantar o banco de dados; Isso significa apenas que o projeto de banco de dados irá verificar se o design de banco de dados é compatível com a plataforma de destino. Para definir a plataforma de destino, abra o **propriedades** para o projeto e selecione **banco de dados SQL do Microsoft Azure** para a plataforma de destino.

![Defina a plataforma de destino](setting-up-database/_static/image2.png)

Você pode criar as tabelas necessárias para este tutorial, adicionando scripts SQL que definem as tabelas. Clique em seu projeto e adicionar um novo item.

![Adicionar novo item](setting-up-database/_static/image3.png)

Adicione uma nova tabela nomeada aluno.

![Adicionar tabela aluno](setting-up-database/_static/image4.png)

No arquivo de tabela, substitua o comando T-SQL com o código a seguir para criar a tabela.

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

Observe que a janela de design sincroniza automaticamente com o código. Você pode trabalhar com o código ou o designer.

![Mostrar código e design](setting-up-database/_static/image5.png)

Adicione outra tabela. Desta vez Nomeie-o curso e use o seguinte comando T-SQL.

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

E, então, repetir mais uma vez para criar uma tabela chamada de registro.

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

Você pode preencher seu banco de dados com dados por meio de um script que é executado depois que o banco de dados é implantado. Adicione um Script de pós-implantação ao projeto. Você pode usar o nome padrão.

![adicionar script pós-implantação](setting-up-database/_static/image6.png)

Adicione o seguinte código T-SQL para o script de pós-implantação. Esse script simplesmente adiciona dados ao banco de dados quando nenhum registro correspondente for encontrado. Não substituir ou excluir quaisquer dados que talvez você tenha inserido no banco de dados.

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

É importante observar que o script de pós-implantação é executado sempre que você implanta seu projeto de banco de dados. Portanto, você precisa considerar cuidadosamente suas necessidades ao escrever este script. Em alguns casos, talvez seja conveniente iniciar a partir um conjunto conhecido de dados toda vez que o projeto é implantado. Em outros casos, talvez não queira alterar os dados existentes de qualquer forma. De acordo com suas necessidades, você pode decidir se é necessário um script de pós-implantação ou o que você precisa incluir no script. Para obter mais informações sobre a população de seu banco de dados com um script de pós-implantação, consulte [incluindo dados em um projeto de banco de dados do SQL Server](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).

Agora você tem arquivos de script SQL 4, mas nenhuma tabela real. Você está pronto para implantar seu projeto de banco de dados localdb. No Visual Studio, clique no botão Iniciar (ou F5) para compilar e implantar seu projeto de banco de dados. Verifique a guia de saída para verificar se a compilação e implantação foi bem-sucedida.

![Mostrar saída](setting-up-database/_static/image7.png)

Para ver que o novo banco de dados foi criado, abra **Pesquisador de objetos do SQL Server** e procure o nome do projeto no servidor de banco de dados local correto (nesse caso **\ProjectsV12 (localdb)**).

![Mostrar o novo banco de dados](setting-up-database/_static/image8.png)

Para ver que as tabelas são populadas com dados, uma tabela com o botão direito e selecione **exibir dados**.

![Mostrar dados da tabela](setting-up-database/_static/image9.png)

Uma exibição editável dos dados da tabela é exibida.

![Mostrar resultados de dados de tabela](setting-up-database/_static/image10.png)

Seu banco de dados agora está configurado e preenchido com dados. O próximo tutorial, você criará um aplicativo web para o banco de dados.

> [!div class="step-by-step"]
> [Avançar](creating-the-web-application.md)
