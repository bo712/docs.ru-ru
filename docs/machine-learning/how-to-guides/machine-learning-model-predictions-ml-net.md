---
title: Прогнозирование с помощью обученной модели
description: Сведения о прогнозировании с помощью обученной модели
ms.date: 05/03/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: dac3b3bfa68776975a2e5e762f46db16e39d61fb
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065607"
---
# <a name="make-predictions-with-a-trained-model"></a>Прогнозирование с помощью обученной модели

Сведения об использовании обученной модели для прогнозирования

## <a name="create-data-models"></a>Создание моделей данных

### <a name="input-data"></a>Входные данные

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

### <a name="output-data"></a>Выходные данные

Как в случае с именами входных столбцов `Features` и `Label`, ML.NET использует имена по умолчанию для столбцов прогнозируемых значений, создаваемых моделью. Имя может отличаться в зависимости от задачи.

Так как в этом примере используется алгоритм линейной регрессии, имя по умолчанию выходного столбца имеет значение `Score`, которое определяется атрибутом [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) в свойстве `PredictedPrice`.

```csharp
class HousingPrediction : HousingData
{
    [ColumnName("Score")]
    public float PredictedPrice { get; set; }
}
```

Модель данных `HousingPrediction` наследует от `HousingData`, чтобы упростить процесс визуализации исходных входных данных, а также выходных данных модели.  

## <a name="set-up-a-prediction-pipeline"></a>Настройка конвейера прогнозирования

Выполняется ли отдельный или пакетный прогноз, конвейер прогнозирования нужно загрузить в приложение. Этот конвейер содержит как преобразования для предварительной обработки данных, так и обученную модель. Приведенный ниже фрагмент кода загружает конвейер прогнозирования из файла с именем `model.zip`.

```csharp
//Create MLContext 
MLContext mlContext = new MLContext();

// Load Trained Model
DataViewSchema predictionPipelineSchema;
ITransformer predictionPipeline = mlContext.Model.Load("model.zip", out predictionPipelineSchema);
```

## <a name="single-prediction"></a>Отдельный прогноз

Чтобы создать отдельный прогноз, создайте [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) с помощью загруженного конвейера прогнозирования.

```csharp
// Create PredictionEngines
PredictionEngine<HousingData, HousingPrediction> predictionEngine = mlContext.Model.CreatePredictionEngine<HousingData, HousingPrediction>(predictionPipeline);
```

Затем с помощью метода [`Predict`](xref:Microsoft.ML.PredictionEngineBase%602.Predict*) передайте входные данные как параметр. Обратите внимание, что для использования метода [`Predict`](xref:Microsoft.ML.PredictionEngineBase%602.Predict*) не нужно, чтобы входные данные были [`IDataView`](xref:Microsoft.ML.IDataView). Это обусловлено тем, что он беспрепятственно осуществляет внутреннюю обработку типов входных данных, чтобы вы могли передать объект типа входных данных. Кроме того, так как `CurrentPrice` является целью или меткой, которую вы пытаетесь спрогнозировать с помощью новых данных, предполагается, что на данный момент значения для него нет.

```csharp
// Input Data
HousingData inputData = new HousingData
{
    Size = 900f,
    HistoricalPrices = new float[] { 155000f, 190000f, 220000f }
};

// Get Prediction
HousingPrediction prediction = predictionEngine.Predict(inputData);
```

При обращении к свойству `Score` объекта `prediction` вы должны получить значение, аналогичное `150079`.

## <a name="batch-prediction"></a>Пакетный прогноз

Получив следующие данные, загрузите их в [`IDataView`](xref:Microsoft.ML.IDataView). Так как `CurrentPrice` является целью или меткой, которую вы пытаетесь спрогнозировать с помощью новых данных, предполагается, что на данный момент значения для него нет.

```csharp
// Actual data
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f,175000f,210000f }
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f }
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f }
    }
};
```

Затем воспользуйтесь методом [`Transform`](xref:Microsoft.ML.ITransformer.Transform*), чтобы применить преобразования данных и сформировать прогнозы.

```csharp
// Predicted Data
IDataView predictions = predictionPipeline.Transform(inputData);
```

Проверьте прогнозируемые значения с помощью метода [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn*).

```csharp
// Get Predictions
float[] scoreColumn = predictions.GetColumn<float>("Score").ToArray();
```

Прогнозируемые значения в столбце оценки должны выглядеть следующим образом:

| Наблюдение | Прогноз |
|---|---|
| 1 | 144 638,2 |
| 2 | 150 079,4 |
| 3 | 107 789,8 |
