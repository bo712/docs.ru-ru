---
title: Преобразования данных
description: Изучите компоненты проектирования признаков, поддерживаемые в ML.NET.
author: natke
ms.author: nakersha
ms.date: 04/02/2019
ms.openlocfilehash: 7ea06e19b4651017079a6ae57136f033e0ce981c
ms.sourcegitcommit: 682c64df0322c7bda016f8bfea8954e9b31f1990
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/13/2019
ms.locfileid: "65558015"
---
# <a name="data-transformations"></a>Преобразования данных

Преобразования используются для подготовки данных, применяемых при обучении модели. В этом руководстве рассматриваются преобразования, которые возвращают классы, реализующие интерфейс [IEstimator](xref:Microsoft.ML.IEstimator%601). Преобразования данных можно соединять в цепочки. Каждое преобразование принимает и выводит данные определенных типов и форматов, которые указаны в связанной справочной документации.

Некоторым преобразованиям данных требуются данные для обучения, чтобы вычислять их параметры. Например, преобразователь <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> позволяет вычислить среднее значение и дисперсию данных для обучения при выполнении операции `Fit()` и использует эти параметры в операции `Transform()`. 

Другим преобразованиям данных не требуются данные для обучения. Например, преобразование <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale*> позволяет выполнять операцию `Transform()` без изучения данных для обучения при выполнении операции `Fit()`.

## <a name="column-mapping-and-grouping"></a>Сопоставление и группирование столбцов

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate%2A> | Объединение одного или нескольких входных столбцов в новый выходной столбец |
| <xref:Microsoft.ML.TransformExtensionsCatalog.CopyColumns%2A> | Копирование и переименование одного или нескольких входных столбцов |
| <xref:Microsoft.ML.TransformExtensionsCatalog.DropColumns%2A> | Удаление одного или нескольких входных столбцов |
| <xref:Microsoft.ML.TransformExtensionsCatalog.SelectColumns%2A> | Выбор одного или нескольких столбцов для хранения входных данных |

## <a name="normalization-and-scaling"></a>Нормализация и масштабирование

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> | Вычитание среднего значения (данные для обучения) и деление на значение дисперсии (данные для обучения) |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLogMeanVariance%2A> | Нормализация на основе логарифма данных для обучения |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLpNorm%2A> | Масштабирование входных векторов на основе [lp-norm](https://en.wikipedia.org/wiki/Lp_space#The_p-norm_in_finite_dimensions), где p — 1, 2 или бесконечность. Значение по умолчанию — норма l2 (Евклидово расстояние) |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeGlobalContrast%2A> | Масштабирование каждого значения в строке путем вычитания среднего значения данных в строке и деления либо на стандартное отклонение, либо на норму l2 (данных в строке) и умножения на настраиваемый коэффициент масштабирования (значение по умолчанию — 2) |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning%2A> | Назначение двоичного индекса в качестве входного значения и деление на число ячеек для получения значения с плавающей запятой от 0 до 1. Границы ячеек вычисляются для равномерного распределения между ними данных для обучения |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeSupervisedBinning%2A> | Назначьте входное значение для ячейки в зависимости от корреляции со столбцом меток |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax%2A> | Масштабирование входных значений на основе разницы между минимальным и максимальным значениями в данных для обучения |

## <a name="conversions-between-data-types"></a>Преобразования между типами данных

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.ConvertType%2A> | Преобразование типа входного столбца в новый тип |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValue*> | Сопоставление значений с ключами (категориями) на основе предоставленного словаря сопоставлений |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey*> | Сопоставление значений с ключами (категориями) путем создания сопоставлений на основе входных данных |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToValue*> | Обратное преобразование ключей в исходное значение |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToVector*> | Обратное преобразование ключей в векторы исходных значений |
| <xref:Microsoft.ML.ConversionsCatalog.MapKeyToBinaryVector*> | Обратное преобразование ключей в двоичный вектор исходных значений |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.Hash*> | Хэширование значения во входном столбце |

## <a name="text-transformations"></a>Преобразования текста

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.TextCatalog.FeaturizeText*> | Преобразование текстового столбца в массив float счетчиков нормализованных n-грамм и символьных n-грамм | 
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoWords*> | Разбиение одного или нескольких текстовых столбцов на отдельные слова |
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoCharactersAsKeys*> | Разбиение одного или нескольких текстовых столбцов на отдельные массивы float в пределах набора тем |
| <xref:Microsoft.ML.TextCatalog.NormalizeText*> | Изменение регистра, удаление диакритических знаков, знаков препинания и цифр |
| <xref:Microsoft.ML.TextCatalog.ProduceNgrams*> | Преобразование текстового столбца в контейнер n-грамм (ряд последовательных слов)|
| <xref:Microsoft.ML.TextCatalog.ProduceWordBags*> | Преобразование текстового столбца в контейнер векторов n-грамм |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedNgrams*> | Преобразование текстового столбца в вектор счетчиков хэшированных n-грамм |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedWordBags*> | Преобразование текстового столбца в контейнер счетчиков хэшированных n-грамм |
| <xref:Microsoft.ML.TextCatalog.RemoveDefaultStopWords*>  | Удаление стоп-слов по умолчанию для указанного языка из входных столбцов |
| <xref:Microsoft.ML.TextCatalog.RemoveStopWords*> | Удаление указанного стоп-слова из входных столбцов |
| <xref:Microsoft.ML.TextCatalog.LatentDirichletAllocation*> | Преобразование документа (в виде вектора значений с плавающей запятой) в вектор значений с плавающей запятой на основе набора тем |
| <xref:Microsoft.ML.TextCatalog.ApplyWordEmbedding*> | Преобразование векторов токенов текста в векторы предложений с помощью предварительно обученной модели |

## <a name="image-transformations"></a>Преобразование изображений

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale*> | Преобразование изображения в оттенки серого |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToImage*> | Преобразование вектора пикселей в <xref:Microsoft.ML.Transforms.Image.ImageDataViewType> |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels*> | Преобразование пикселей из входного изображения в вектор чисел |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages*> | Загрузка изображений из папки в память |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages*> | Изменение размеров изображений |

## <a name="categorical-data-transformations"></a>Преобразование категориальных данных

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*> | Преобразование одного или нескольких текстовых столбцов в векторы с использованием [прямой](https://en.wikipedia.org/wiki/One-hot) кодировки |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotHashEncoding*> | Преобразование одного или нескольких текстовых столбцов в векторы с использованием прямой кодировки на основе хэша |

## <a name="missing-values"></a>Отсутствующие значения

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.ExtensionsCatalog.IndicateMissingValues*> | Создание логического выходного столбца, который будет иметь значение true, если во входном столбце не указано значение |
| <xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*> | Создание выходного столбца, значение которого будет задано по умолчанию, если отсутствует значение из входного столбца. В противном случае по умолчанию будет задано значение из входного столбца. |

## <a name="feature-selection"></a>Выбор признаков

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnCount*> | Выбор признаков, у которых значения, заданные не по умолчанию, превышают порог |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnMutualInformation*> | Выбор признаков, от которых больше всего зависят данные в столбце метки |

## <a name="custom-transformations"></a>Пользовательские преобразования

| Transform | Определение |
| --- | --- |
| <xref:Microsoft.ML.CustomMappingCatalog.CustomMapping*> | Преобразование существующих столбцов в новые с помощью пользовательского сопоставления |
