# Cравнение CoT и ансамбля CoT на GSM8K с BLOOM-7B 

В рамках данного проекта было проведено сравнение результатов CoT и ансамблированного CoT для модели BLOOM-7B. 

Было решено использовать эту модель вместо BLOOM-176B, так как последняя была очень долгое время недоступна из-за технических проблем, из-за чего было невозможно сгенерировать достаточно данных.

<img src="broken.png" width="300" />




Модель BLOOM-7B имеет относительно малый масштаб, особенно для сложных задач в области машинного обучения. Однако, несмотря на это, модель все же продемонстрировала некоторую эффективность в решении поставленной задачи. Нам удалось сгенерировать по 15 сэмплов для 100 задач. Конечно, это недостаточное количество для полноценного статистического анализа, но мы все равно провели интересные исследования на этих данных.

| Модель | Accuracy | 
| -------- | -------- |
| LaMDA 8B | 1.6 | 
| GPT 6.7B | 2.4 |
| PaLM 8B | 4.1 | 
| BLOOM 7B| 2 | 


Были проведены эксперименты, в результате которых мы обнаружили, что ансамбль дал удивительный результат - правильный ответ был сгенерирован целых 13 раз. Правда, почти во всех случаях этот ответ не был выбран, потому что оказался не самым частым в ансамбле. Но вероятность "угадать" ответ на задачу очень мала, поэтому результаты эксперимента могут указывать на то, что модель действительно научилась некоторым характеристикам языка и смогла применить их для решения задачи.

Кроме сравнения результатов CoT и ансамбля CoT также было проведено сравнение векторизаций решений, которые сгенерировала модель BLOOM-7B. Для этого использована SBERT - модель для генерации векторных представлений предложений и текстов.

Мы векторизовали рассуждения, которые были сгенерированы моделью, и посчитали расстояние между вектором сгенерированного решения и эталонного. Для СоТ считалось расстояние от правильного рассуждения до вектора средних арифметических ансамбля решений.

Результаты оказались поразительными. Среднее расстояние для простого CoT было равно 60, что означает, что векторизованные рассуждения отличались друг от друга весьма существенно. Однако среднее расстояние для вектора средних арифметических по ансамблю оказалось близко к 3, что говорит о том, что рассуждения похожи на правильные. Если бы возможно было "слепить" среднее решение из рассуждений модели, то оно бы оказалось очень близко к эталонному :sparkles:




<img src="distance.png" width="700" />

В целом, результаты наших экспериментов показывают, что даже такая маленькая модель, как BLOOM-7B, может дать достаточно любопытные результаты :)



:pig: О трудностях:

Пока BLOOM-176B функционировала, были сделаны несколько попыток генерации решений с её помощью. В отличие от BLOOM-7B, тексты, сгенерированные BLOOM-176B, были более похожи на человеческие. Но время генерации решений с использованием этой модели было очень долгим (одно решение генерировалось более пяти минут, а это слишком медленно для решения задачи с помощью ансамблированного СоТ)

Также были предприняты попытки генерации решений с использованием huggingface, однако, там существует очень маленький лимит бесплатных генераций, что сильно усложняет процесс. 

Работа с моделью была затруднена техническими ограничениями Google Colab, в частности, ограничением времени использования GPU и необходимостью переключения между аккаунтами (было создано 15 аккаунтов) 
