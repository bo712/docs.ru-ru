---
title: Обучение и оценка модели машинного обучения с использованием кросс-валидации
description: Обучение и оценка модели машинного обучения с использованием кросс-валидации
ms.date: 05/03/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: a06711ca83ea545adc7292cf6d8173f006fdb94d
ms.sourcegitcommit: 682c64df0322c7bda016f8bfea8954e9b31f1990
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/13/2019
ms.locfileid: "65557836"
---
# <a name="train-and-evaluate-a-machine-learning-model-using-cross-validation"></a>Обучение и оценка модели машинного обучения с использованием кросс-валидации

Узнайте, как использовать кросс-валидацию для создания более надежных моделей машинного обучения в ML.NET. 

Кросс-валидация — это методика обучения и оценки модели, которая разбивает данные на несколько секций и обучает несколько алгоритмов на этих секциях. Этот метод повышает надежность модели, удерживая данные вне процесса обучения. Кроме повышения производительности на многих неучитываемых наблюдениях, в средах с ограниченными данными он может быть эффективным инструментом для обучения моделей с меньшим набором данных.

## <a name="the-data-and-data-model"></a>Данные и модель данных

Используя данные из файла, который имеет следующий формат:

```text
Size (Sq. ft.), HistoricalPrice1 ($), HistoricalPrice2 ($), HistoricalPrice3 ($), Current Price ($)
620.00, 148330.32, 140913.81, 136686.39, 146105.37
550.00, 557033.46, 529181.78, 513306.33, 548677.95
1127.00, 479320.99, 455354.94, 441694.30, 472131.18
1120.00, 47504.98, 45129.73, 43775.84, 46792.41
```

Можно моделировать данные с помощью класса, например `HousingData`:

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }
 
    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

Загрузка данных в [`IDataView`](xref:Microsoft.ML.IDataView):

## <a name="prepare-the-data"></a>Подготовка данных

Следует предварительно обработать данные перед их использованием для создания модели машинного обучения. В этом примере столбцы `Size` и `HistoricalPrices` объединяются в один вектор признака, который выводится в новый столбец с именем `Features` с помощью метода [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*). Кроме получения данных в формате, ожидаемом алгоритмами ML.NET, сцепка столбцов оптимизирует последующие операции в конвейере, применяя операцию один раз для объединенного столбца, а не обрабатывая каждый отдельный столбец. 

Как только столбцы объединяются в один вектор, [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*) применяется к столбцу `Features`, чтобы получить `Size` и `HistoricalPrices` в одном и том же диапазоне 0–1. 

```csharp
// Define data prep estimator
IEstimator<ITransformer> dataPrepEstimator = 
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data prep transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// Transform data
IDataView transformedData = dataPrepTransformer.Transform(data);
```

## <a name="train-model-with-cross-validation"></a>Обучение модели с помощью кросс-валидации

Когда данные предварительно обработаны, пришло время для обучения модели. Во-первых, выберите алгоритм, который наиболее точно соответствует задаче машинного обучения. Поскольку прогнозируемое значение является числовым и непрерывным, задача — регрессия. Один из алгоритмов регрессии, реализуемый ML.NET, – алгоритм [`StochasticDualCoordinateAscentCoordinator`](xref:Microsoft.ML.Trainers.SdcaRegressionTrainer). Для обучения модели с использованием кросс-валидации используется метод [`CrossValidate`](xref:Microsoft.ML.RegressionCatalog.CrossValidate*). 

> [!NOTE]
> Несмотря на то что в этом примере используется модель линейной регрессии, CrossValidate применяется для всех других задач машинного обучения в ML.NET, за исключением обнаружения аномалий.

```csharp
// Define StochasticDualCoordinateAscent algorithm estimator
IEstimator<ITransformer> sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Apply 5-fold cross validation
var cvResults = mlContext.Regression.CrossValidate(transformedData, sdcaEstimator, numberOfFolds: 5);
```

[`CrossValidate`](xref:Microsoft.ML.RegressionCatalog.CrossValidate*) выполняет следующие действия.

1. Разбивает данные на несколько секций по значению, указанному в параметре `numberOfFolds`. В результате каждая секция превратится в объект [`TrainTestData`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestData).
1. Модель обучается на каждой из секций с помощью указанного алгоритма оценки машинного обучения в наборе данных для обучения.
1. Эффективность каждой модели оценивается с помощью метода [`Evaluate`](xref:Microsoft.ML.RegressionCatalog.Evaluate*) на тестовом наборе данных. 
1. Для всех моделей возвращается сама модель, а также ее метрики.

Результат в `cvResults` сохраняется в коллекции объектов [`CrossValidationResult`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601). Этот объект включает обученную модель, а также метрики, доступные через свойства [`Model`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601.Model) и [`Metrics`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601.Metrics) соответственно. В этом примере свойство `Model` имеет тип [`ITransformer`](xref:Microsoft.ML.ITransformer), а свойство `Metrics` имеет тип [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics). 

## <a name="extract-metrics"></a>Извлечение метрик

Метрики для разных обученных моделей доступны через свойства `Metrics` отдельного объекта [`CrossValidationResult`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601). В этом случае [метрика R-квадрат](https://en.wikipedia.org/wiki/Coefficient_of_determination) извлекается и сохраняется в переменной `rSquared`. 

```csharp
IEnumerable<double> rSquared = 
    cvResults
        .Select(fold => fold.Metrics.RSquared);
```

Если проверить содержимое переменной `rSquared`, в выходных данных должно быть пять значений в диапазоне от 0 до 1, где близость к 1 означает, что эта модель лучше.

## <a name="select-the-best-performing-model"></a>Выбор наиболее эффективной модели

С помощью таких метрик, как R-квадрат, отранжируйте модели от лучших к наихудшим. Затем выберите лучшую модель для прогнозов или дополнительных операций.

```csharp
// Select all models
ITransformer[] models =
    cvResults
        .OrderByDescending(fold => fold.Metrics.RSquared)
        .Select(fold => fold.Model)
        .ToArray();

// Get Top Model
ITransformer topModel = models[0];
```
