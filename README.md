import random
import math

def sigmoid(x):
    return 1 / (1 + math.exp(-x))

# --- ДАТАСЕТ (наши машины) ---
# [Клиренс, Объем движка, Объем багажника, Лошадиные силы]
dataset = [
    [20.0, 2.0, 500.0, 150.0],  # кроссовер
    [15.0, 1.6, 400.0, 120.0],  # седан
    [25.0, 3.0, 600.0, 250.0],  # внедорожник
    [10.0, 1.4, 300.0, 90.0]    # хэтчбек
]

print("1. Простой нейрон")
x1, x2, x3 = dataset[0][0], dataset[0][1], dataset[0][2]
w1, w2, w3 = 0.2, 0.8, -0.5
summa = x1*w1 + x2*w2 + x3*w3
print("Результат:", sigmoid(summa))
print("-" * 20)

print("2. Нейронная сеть")
vhod = dataset[0][:2]
w_h1 = [0.1, 0.2]
w_h2 = [0.3, 0.4]
w_h3 = [0.5, 0.6]
h1 = sigmoid(vhod[0]*w_h1[0] + vhod[1]*w_h1[1])
h2 = sigmoid(vhod[0]*w_h2[0] + vhod[1]*w_h2[1])
h3 = sigmoid(vhod[0]*w_h3[0] + vhod[1]*w_h3[1])
w_out = [0.7, 0.8, 0.9]
res = sigmoid(h1*w_out[0] + h2*w_out[1] + h3*w_out[2])
print("Ответ:", res)
print("-" * 20)

print("3. Определение типа кузова (проходим по датасету)")
w_c1 = [random.uniform(0, 1) for _ in range(3)]
w_c2 = [random.uniform(0, 1) for _ in range(3)]
w_c3 = [random.uniform(0, 1) for _ in range(3)]
w_c_out = [random.uniform(0, 1) for _ in range(3)]
for i in range(len(dataset)):
    car = dataset[i][:3]
    ch1 = sigmoid(car[0]*w_c1[0] + car[1]*w_c1[1] + car[2]*w_c1[2])
    ch2 = sigmoid(car[0]*w_c2[0] + car[1]*w_c2[1] + car[2]*w_c2[2])
    ch3 = sigmoid(car[0]*w_c3[0] + car[1]*w_c3[1] + car[2]*w_c3[2])
    res_car = sigmoid(ch1*w_c_out[0] + ch2*w_c_out[1] + ch3*w_c_out[2])
    print("Машина", i+1, "-> вероятность внедорожника:", round(res_car, 4))
print("-" * 20)

print("4. Добавляем лошадиные силы (незначащий параметр)")
w_c1_new = [random.uniform(0, 1), random.uniform(0, 1), random.uniform(0, 1), 0.001]
w_c2_new = [random.uniform(0, 1), random.uniform(0, 1), random.uniform(0, 1), 0.001]
w_c3_new = [random.uniform(0, 1), random.uniform(0, 1), random.uniform(0, 1), 0.001]
w_c_out_new = [random.uniform(0, 1) for _ in range(3)]
for i in range(len(dataset)):
    car = dataset[i]
    ch1_new = sigmoid(car[0]*w_c1_new[0] + car[1]*w_c1_new[1] + car[2]*w_c1_new[2] + car[3]*w_c1_new[3])
    ch2_new = sigmoid(car[0]*w_c2_new[0] + car[1]*w_c2_new[1] + car[2]*w_c2_new[2] + car[3]*w_c2_new[3])
    ch3_new = sigmoid(car[0]*w_c3_new[0] + car[1]*w_c3_new[1] + car[2]*w_c3_new[2] + car[3]*w_c3_new[3])
    res_car_new = sigmoid(ch1_new*w_c_out_new[0] + ch2_new*w_c_out_new[1] + ch3_new*w_c_out_new[2])
    print("Машина", i+1, "-> с лошадиными силами:", round(res_car_new, 4))
print("-" * 20)

print("5. Итоговая сеть с двумя скрытыми слоями (по датасету)")
w1_1 = [random.uniform(0, 1) for _ in range(4)]
w1_2 = [random.uniform(0, 1) for _ in range(4)]
w1_3 = [random.uniform(0, 1) for _ in range(4)]
w1_4 = [random.uniform(0, 1) for _ in range(4)]
w2_1 = [random.uniform(0, 1) for _ in range(4)]
w2_2 = [random.uniform(0, 1) for _ in range(4)]
w2_3 = [random.uniform(0, 1) for _ in range(4)]
w_out_final = [random.uniform(0, 1) for _ in range(3)]

for i in range(len(dataset)):
    x = dataset[i]
    h1_1 = sigmoid(x[0]*w1_1[0] + x[1]*w1_1[1] + x[2]*w1_1[2] + x[3]*w1_1[3])
    h1_2 = sigmoid(x[0]*w1_2[0] + x[1]*w1_2[1] + x[2]*w1_2[2] + x[3]*w1_2[3])
    h1_3 = sigmoid(x[0]*w1_3[0] + x[1]*w1_3[1] + x[2]*w1_3[2] + x[3]*w1_3[3])
    h1_4 = sigmoid(x[0]*w1_4[0] + x[1]*w1_4[1] + x[2]*w1_4[2] + x[3]*w1_4[3])
    layer1 = [h1_1, h1_2, h1_3, h1_4]
    
    h2_1 = sigmoid(layer1[0]*w2_1[0] + layer1[1]*w2_1[1] + layer1[2]*w2_1[2] + layer1[3]*w2_1[3])
    h2_2 = sigmoid(layer1[0]*w2_2[0] + layer1[1]*w2_2[1] + layer1[2]*w2_2[2] + layer1[3]*w2_2[3])
    h2_3 = sigmoid(layer1[0]*w2_3[0] + layer1[1]*w2_3[1] + layer1[2]*w2_3[2] + layer1[3]*w2_3[3])
    layer2 = [h2_1, h2_2, h2_3]
    
    res_final = sigmoid(layer2[0]*w_out_final[0] + layer2[1]*w_out_final[1] + layer2[2]*w_out_final[2])
    print("Машина", i+1, "-> итог:", round(res_final, 4))
