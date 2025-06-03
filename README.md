# Anomaly-Detection-in-Transactions
Обнаружение аномалий в транзакциях означает выявление необычных или неожиданных закономерностей в транзакциях или связанных с ними действиях. Эти закономерности, известные как аномалии или выбросы, значительно отклоняются от ожидаемой нормы и могут указывать на нерегулярное или мошенническое поведение <p>
Описание датасета:
- Transaction_ID: уникальный идентификатор для каждой транзакции.
- Transaction_Amount: сумма транзакции.
- Transaction_Volume: количество или число товаров/действий, вовлеченных в транзакцию.
- Average_Transaction_Amount: историческая средняя сумма транзакции для счета.
- Frequency_of_Transactions: как часто транзакции обычно выполняются счетом.
- Time_Since_Last_Transaction: время, прошедшее с момента последней транзакции.
- Day_of_Week: день недели, когда была совершена транзакция.
- Time_of_Day: время суток, когда была совершена транзакция.
- Age: возраст владельца счета.
- Gender: пол владельца счета.
- Income: доход владельца счета.
- Account_Type: тип счета (например, личный, деловой).
# посмотрим на распределение количества транзакций в данных:
![distribution_of_transaction_amount](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/distribution_of_transaction_amount.png)<p>
# распределение сумм транзакций по типу счета: <p>
![Transaction Amount by Account Type.png](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/Transaction%20Amount%20by%20Account%20Type.png)<p>
# средняя сумма транзакции по возрасту:
![Average Transaction Amount vs. Age.png](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/Average%20Transaction%20Amount%20vs.%20Age.png)<p>
Разницы в средней сумме транзакции по возрасту нет <p>
# количество транзакций по дням недели:
![Count of Transactions by Day of the Week.png](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/Count%20of%20Transactions%20by%20Day%20of%20the%20Week.png)
# корреляция между всеми столбцами данных:
![Correlation Heatmap.png](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/Correlation%20Heatmap.png)
# визуализация аномалий в данных:
![Anomalies in Transaction Amount.png](https://github.com/Mamaeva-Bariyat/Anomaly-Detection-in-Transactions/blob/main/images/Anomalies%20in%20Transaction%20Amount.png)
# Modeling <p>
model = IsolationForest(contamination=0.02, random_state=42) <p>
Отчет о производительности <p>
        precision    recall  f1-score   support

      Normal       1.00      1.00      1.00       196
     Anomaly       1.00      1.00      1.00         4

    accuracy                           1.00       200
    macro avg       1.00      1.00     1.00       200
    weighted avg    1.00      1.00     1.00       200 <p>
    
# Прогноз пользователя <p>
создан скрпит, который принимает пользовательский ввод для трех признаков и возвращает, является ли транзакция нормальной или аномальной.<p>

relevant_features = ['Transaction_Amount', 'Average_Transaction_Amount', 'Frequency_of_Transactions']


user_inputs = []<p>
for feature in relevant_features:<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user_input = float(input(f"Enter the value for '{feature}': "))<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;user_inputs.append(user_input)<p>

user_df = pd.DataFrame([user_inputs], columns=relevant_features)<p>


user_anomaly_pred = model.predict(user_df)<p>

user_anomaly_pred_binary = 1 if user_anomaly_pred == -1 else 0<p>


if user_anomaly_pred_binary == 1:<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;print("Anomaly detected: This transaction is flagged as an anomaly.")<p>
else:<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;print("No anomaly detected: This transaction is normal.")<p>

