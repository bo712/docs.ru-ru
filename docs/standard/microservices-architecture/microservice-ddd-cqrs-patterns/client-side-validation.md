---
title: Проверка на стороне клиента (проверка на уровнях представления)
description: Архитектура микрослужб .NET для контейнерных приложений .NET | Ключевые понятия проверки на стороне клиента.
ms.date: 10/08/2018
ms.openlocfilehash: 4e72dcafafc3144a75afe1fd23a4a779f5667459
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644840"
---
# <a name="client-side-validation-validation-in-the-presentation-layers"></a>Проверка на стороне клиента (проверка на уровнях представления)

Даже если источником истины является модель предметной области и в конечном итоге необходимо проводить проверки на этом уровне, проверку можно выполнить как на уровне модели предметной области (на сервере), так и на уровне интерфейса пользователя (на клиенте).

Проверка на стороне клиента очень удобна для пользователей. Она экономит время, которое в противном случае тратилось бы на круговой путь к серверу, в результате которого выдавались бы ошибки проверки. С точки зрения бизнеса даже доли секунды, умножаемые в сотни раз каждый день, позволяют значительно сократить расходуемое время, деньги и усилия. Простая и немедленная проверка позволяет пользователям работать эффективнее и повышает точность входных и выходных данных.

Так же как модель представления отличается от модели предметной области, проверка модели представления и проверка модели предметной области имеют сходные черты, но выполняют разные функции. Если вы беспокоитесь о принципе DRY ("Не повторяйся"), то в этом случае повторное использование кода может означать взаимозависимость, а в корпоративном приложении взаимозависимость стороны сервера и стороны клиента гораздо хуже, чем нарушение принципа "Не повторяйся".

Даже при проведении проверки на стороне клиента следует всегда проверять команды или входящие объекты переноса данных в серверном коде, ведь API сервера являются возможным вектором атаки. Как правило, рекомендуется выполнять обе проверки, поскольку, с точки зрения взаимодействия с пользователем, в клиентском приложении лучше действовать на опережение и не допускать ввод пользователем недопустимых данных.

Поэтому в коде на стороне клиенты вы обычно проверяете модели представления. Можно также проверять исходящие объекты переноса данных или команды клиента, прежде чем отправлять их службам.

Выполнение проверки на стороне клиента зависит от типа создаваемого клиентского приложения. Существуют отличия при проверке данных в веб-приложениях MVC, в которых программирование по большей части осуществляется в .NET, веб-приложениях SPA, в которых проверка написана на JavaScript или TypeScript, и в мобильных приложениях с кодом на Xamarin и C#.

## <a name="additional-resources"></a>Дополнительные ресурсы

### <a name="validation-in-xamarin-mobile-apps"></a>Проверка в мобильных приложениях Xamarin

- **Проверка текстового ввода и отображение ошибок** \
  [https://developer.xamarin.com/recipes/ios/standard\_controls/text\_field/validate\_input/](https://developer.xamarin.com/recipes/ios/standard_controls/text_field/validate_input/)

- **Ответный вызов проверки** \
  <https://developer.xamarin.com/samples/xamarin-forms/XAML/ValidationCallback/>

### <a name="validation-in-aspnet-core-apps"></a>Проверка в приложениях ASP.NET Core

- **Рик Андерсон (Rick Anderson). Добавление проверки** \
  <https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation>

### <a name="validation-in-spa-web-apps-angular-2-typescript-javascript"></a>Проверка в веб-приложениях SPA (Angular 2, TypeScript, JavaScript)

- **Адо Кукич (Ado Kukic). Проверка форм Angular 2** \
  <https://scotch.io/tutorials/angular-2-form-validation>

- **Проверка форм** \
  <https://angular.io/guide/form-validation>

- **Проверка.** Документация Breeze. \
  <https://breeze.github.io/doc-js/validation.html>

Подытожим основные принципы проверки:

- Сущности и агрегаты должны обеспечивать собственную согласованность и всегда быть допустимыми. Агрегатные корни отвечают за согласованность нескольких сущностей в одном агрегате.

- Если вы считаете, что сущность должна входить в недопустимое состояние, подумайте об использовании другой объектной модели — например, используйте объект переноса данных до создания окончательной сущности предметной области.

- Если необходимо создать несколько связанных объектов, например агрегат, и они будут допустимы только после создания всех объектов, используйте шаблон "фабрика".

- В большинстве случаев избыточная проверка на стороне клиента уместна, ведь приложение может действовать на опережение.

>[!div class="step-by-step"]
>[Назад](domain-model-layer-validations.md)
>[Вперед](domain-events-design-implementation.md)
