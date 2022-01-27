import requests
import random
import string
import time

print(""" F4OURS7VEN - Gerador De Nitro / 
 """)

time.sleep(0.3)
print("Carregando Sistema...\n")
time.sleep(0.2)

num = int(input('Quantos códigos de nitro você quer gerar e checar: '))

with open("Nitro Codes.txt", "w", encoding='utf-8') as file:
    print("Seus códigos de nitro estão sendo gerador, seja paciente.")

    start = time.time()

    for i in range(num):
        code = "".join(
            random.choices(string.ascii_uppercase + string.digits +
                           string.ascii_lowercase,
                           k=16))

        file.write(f"https://discord.gift/{code}\n")

    print(f"Gerandos {num} códigos | Tempo Estimado: {time.time() - start}\n")

with open("Nitro Codes.txt") as file:
    for line in file.readlines():
        nitro = line.strip("\n")

        url = "https://discordapp.com/api/v6/entitlements/gift-codes/" + nitro + "?with_application=false&with_subscription_plan=true"

        r = requests.get(url)

        if r.status_code == 200:
            print(f" Valido | {nitro} ")
            break
        else:
            #should be invalid
            print(f" Invalido | {nitro} ")

print("\nGerando códigos, escolha um numero alto e seja paciente.")

