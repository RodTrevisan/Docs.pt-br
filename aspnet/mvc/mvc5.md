---
uid: mvc/mvc5
title: ASP.NET MVC 5 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 5 ASP.NET MVC 5 é uma estrutura para a criação de aplicativos web escalonáveis baseados em padrões, usando padrões de design bem estabelecidos e o poder do AS....
ms.author: aspnetcontent
ms.date: 01/20/2014
ms.assetid: f79fbf7f-59e5-4279-a832-c1a0294630f4
msc.legacyurl: /mvc/mvc5
msc.type: content
ms.openlocfilehash: 97423f9a2e66187329887c4c5e92bb20cb9a7fc4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814334"
---
<a name="aspnet-mvc-5"></a>ASP.NET MVC 5
====================
## <a name="whats-new-in-aspnet-mvc-5"></a>O que há de novo no ASP.NET MVC 5

### <a name="one-aspnet"></a>Um ASP.NET

Os modelos de projeto Web MVC integração perfeita com a nova experiência do One ASP.NET. Você pode personalizar seu projeto do MVC e configurar a autenticação usando o Assistente de criação de projeto do One ASP.NET. Um tutorial de Introdução ao ASP.NET MVC 5 pode ser encontrado em [Introdução ao ASP.NET MVC 5](overview/getting-started/introduction/getting-started.md).

Para obter informações sobre como atualizar projetos MVC 4 para o MVC 5, consulte [como atualizar um ASP.NET MVC 4 e o projeto de API da Web para ASP.NET MVC 5 e API Web 2](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).

### <a name="aspnet-identity"></a>ASP.NET Identity

Os modelos de projeto do MVC foram atualizados para usar a identidade do ASP.NET para autenticação e gerenciamento de identidade. Um tutorial que contam com autenticação do Facebook e Google e a nova API de associação pode ser encontrado em [criar um aplicativo do ASP.NET MVC 5 com o Facebook e Google OAuth2 e OpenID Sign-on](overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) e [implantar um aplicativo MVC do ASP.NET seguro com Associação, OAuth e banco de dados SQL para um Site da Web do Azure Windows](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

### <a name="bootstrap"></a>Bootstrap

O modelo de projeto do MVC foi atualizado para usar [Bootstrap](http://getbootstrap.com/) para fornecer uma responsiva e elegante aparência que você pode personalizar facilmente. Para obter mais informações, consulte [Bootstrap em modelos de projeto da web do Visual Studio 2013](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap).

### <a name="authentication-filters"></a>Filtros de autenticação

[Filtros de autenticação](http://www.dotnetcurry.com/showarticle.aspx?ID=957) são um novo tipo de filtro no ASP.NET MVC que executam antes de filtros de autorização no pipeline do ASP.NET MVC e permitem que você especifique a autenticação lógica por ação, por controlador ou globalmente para todos os controladores. Filtros de autenticação processam credenciais na solicitação e fornecem uma entidade de segurança correspondente. Filtros de autenticação também podem adicionar desafios de autenticação em resposta a solicitações não autorizadas. Ver [filtros de autenticação do ASP.NET MVC 5](http://www.dotnetcurry.com/showarticle.aspx?ID=957), [filtros de autenticação no ASP.NET MVC 5](http://theshravan.net/blog/authentication-filters-in-asp-net-mvc-5/).

### <a name="filter-overrides"></a>Substituições de filtro

Agora você pode substituir os filtros se aplicam a um controlador ou método de ação em questão, especificando um [substituir filtro](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5). Os filtros de substituição especificarem um conjunto de tipos de filtro que não deve ser executado para um determinado escopo (ação ou controlador). Isso permite que você defina filtros que se aplicam globalmente, mas, em seguida, excluir determinados filtros globais da aplicação a controladores ou ações específicas. Ver [novo filtro substitui o recurso no ASP.NET MVC 5 e API Web ASP.NET 2](https://weblogs.asp.net/imranbaloch/archive/2013/09/25/new-filter-overrides-in-asp-net-mvc-5-and-asp-net-web-api-2.aspx), [como usar o recurso de substituições de filtro do ASP.NET MVC 5](http://hackwebwith.net/how-to-use-the-asp-net-mvc-5-filter-overrides-feature/), e [substituições de filtro no ASP.NET MVC 5](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5)

### <a name="attribute-routing"></a>Roteamento de atributo

ASP.NET MVC agora dá suporte à [roteamento de atributo](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx), graças a uma contribuição por Tim McCall, autor de [ http://attributerouting.net ](http://attributerouting.net). Com o roteamento de atributo, você pode especificar suas rotas, anotando suas ações e controladores.

## <a name="new-web-project-experience"></a>Nova experiência de projeto da Web

Aprimoramos a experiência de criação de novos projetos da web no Visual Studio 2013. No **novo projeto de Web do ASP.NET** caixa de diálogo que você pode selecionar o tipo de projeto que você deseja, configurar qualquer combinação de tecnologias de (Web Forms, MVC, Web API), configurar opções de autenticação e adicionar um projeto de teste de unidade.

![Novo projeto ASP.NET](mvc5/_static/image1.png)

Nova caixa de diálogo permite que você altere as opções de autenticação padrão para muitos dos modelos. Por exemplo, quando você cria um projeto de Web Forms do ASP.NET você pode selecionar qualquer uma das seguintes opções:

- Sem autenticação
- Contas de usuário individuais (associação ASP.NET ou login do provedor social)
- Contas organizacionais (Active Directory em um aplicativo da internet)
- Autenticação do Windows (Active Directory em um aplicativo de intranet)

![Opções de autenticação](mvc5/_static/image2.png)

Para obter mais informações sobre o novo processo para a criação de projetos da web, consulte [Criando projetos Web do ASP.NET no Visual Studio 2013](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md). Para obter mais informações sobre as novas opções de autenticação, consulte [ASP.NET Identity](../identity/overview/index.md).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>Scaffolding do ASP.NET

Scaffolding do ASP.NET é uma estrutura de geração de código para aplicativos Web ASP.NET. Ele torna mais fácil adicionar o código clichê ao seu projeto que interage com um modelo de dados.

Nas versões anteriores do Visual Studio, o scaffolding foi limitado a projetos do ASP.NET MVC. Com o Visual Studio 2013, agora você pode usar o scaffolding para qualquer projeto ASP.NET, incluindo o Web Forms. Visual Studio 2013 oferece suporte para geração de páginas para um projeto de Web Forms, mas você ainda pode usar o scaffolding com Web Forms Adicionando dependências MVC ao projeto. Suporte para a geração de páginas para formulários da Web será adicionado em uma atualização futura.

Ao usar o scaffolding, podemos garantir que todos os dependências estão instaladas no projeto. Por exemplo, se você começa com um projeto de Web Forms do ASP.NET e, em seguida, utilizar o scaffolding para adicionar um controlador da API da Web, os pacotes NuGet necessários e as referências são adicionadas ao seu projeto automaticamente.

Para adicionar o scaffolding do MVC para um projeto de Web Forms, adicione uma **Novo Item de Scaffold** e selecione **dependências do MVC 5** na janela de diálogo. Há duas opções para scaffolding MVC; Mínimo e completo. Se você selecionar no mínimo, apenas os pacotes do NuGet e referências para o ASP.NET MVC são adicionadas ao seu projeto. Se você selecionar a opção completa, as dependências mínimas são adicionadas, bem como os arquivos de conteúdo necessários para um projeto do MVC.

Suporte para scaffolding dos controladores assíncronos usa os novos recursos assíncronos do Entity Framework 6.

Para obter mais informações e tutoriais, consulte [visão geral de Scaffolding do ASP.NET](../visual-studio/overview/2013/aspnet-scaffolding-overview.md).

### <a name="getting-help-and-reporting-issues"></a>Obtendo ajuda e relatar problemas

- [Problemas conhecidos e lista de alterações significativas](../visual-studio/overview/2013/release-notes.md#knownissues)
- Obtenha ajuda e discutir o ASP.NET MVC 5 nos [fóruns](https://forums.asp.net/1146.aspx)
- [Relatar um bug no ASP.NET MVC 5](https://github.com/aspnet/AspNetWebStack/issues)
- [Fazer uma solicitação de recurso](http://aspnet.uservoice.com/forums/41201-asp-net-mvc)

### <a name="upgrading-from-aspnet-mvc-4"></a>Atualizando do ASP.NET MVC 4

Consulte [como atualizar um ASP.NET MVC 4 e Web API do projeto ASP.NET MVC 5 e API Web 2](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)
