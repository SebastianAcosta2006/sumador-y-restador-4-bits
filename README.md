# sumador-y-restador-4-bits
INTRODUCCION

En este proyecto se implementó un sumador y restador binario de 4 bits utilizando el lenguaje Python, con el propósito de simular el comportamiento básico de la lógica digital. El programa está construido a partir del uso de compuertas lógicas AND, OR y NOT, sin emplear directamente operadores aritméticos propios del lenguaje

La operación de suma se realiza mediante el uso de sumadores completos, mientras que la resta se lleva a cabo aplicando el método del complemento a dos. Con este desarrollo se busca comprender cómo las operaciones aritméticas básicas pueden ser representadas y ejecutadas a nivel lógico, reforzando los conceptos estudiados en clase sobre sistemas digitales. El usuario introduce los números binarios a través de la terminal y el programa muestra los resultados de la suma y la resta obtenidos

OBJETIVO

Desarrollar un sumador y restador binario de 4 bits en Python haciendo uso exclusivo de compuertas lógicas AND, OR y NOT, con el fin de entender el funcionamiento interno de las operaciones aritméticas desde el punto de vista de la lógica digital

FUNCIONAMIENTO

El programa solicita al usuario dos números binarios de 4 bits ingresados desde la terminal

En primer lugar, se realiza la suma bit a bit utilizando sumadores completos, teniendo en cuenta la propagación del acarreo (carry) entre cada posición

Para realizar la resta, el segundo número se transforma a su complemento a dos y posteriormente se suma al primer número, obteniendo así el resultado de la operación

RESULTADOS

El programa presenta resultados correctos tanto para la suma como para la resta de números binarios de 4 bits. A continuación, se muestra un ejemplo de la ejecución del programa en el compilador online donde se pueden observar los valores ingresados y los resultados obtenidos

CODIGO
# ----- COMPUERTAS LOGICAS BASICAS -----

def XOR(a, b):
    # devuelve True si solo uno es True
    return a != b


# ----- SUMADOR COMPLETO -----

def full_adder(a, b, cin):
    # suma de los bits
    suma = XOR(XOR(a, b), cin)
    # carry de salida
    carry = (a and b) or (cin and XOR(a, b))
    return suma, carry


# ----- SUMADOR DE 4 BITS -----

def sumador_4_bits(A, B):
    resultado = [False]*4
    carry = False

    # se suma desde el bit menos significativo
    for i in range(3, -1, -1):
        resultado[i], carry = full_adder(A[i], B[i], carry)

    return resultado, carry


# ----- RESTADOR DE 4 BITS -----

def restador_4_bits(A, B):
    # se invierten los bits de B
    B = [not b for b in B]
    # se suma 1 (complemento a dos)
    B, _ = sumador_4_bits(B, [False, False, False, True])
    # se suma A + (-B)
    resultado, _ = sumador_4_bits(A, B)
    return resultado


# ----- CONVERSIONES -----

def str_a_bits(s):
    # convierte string binario a lista booleana
    return [c == '1' for c in s]

def bits_a_str(bits):
    # convierte lista booleana a string binario
    return ''.join('1' if b else '0' for b in bits)


# ----- VALIDACION -----

def validar_binario_4(s):
    # valida que tenga 4 bits y solo 0 o 1
    return len(s) == 4 and all(c in '01' for c in s)


# ----- PROGRAMA PRINCIPAL -----

A_str = input("Ingrese A (4 bits): ")
while not validar_binario_4(A_str):
    A_str = input("Invalido. Ingrese A (4 bits): ")

B_str = input("Ingrese B (4 bits): ")
while not validar_binario_4(B_str):
    B_str = input("Invalido. Ingrese B (4 bits): ")

# conversion a bits
A = str_a_bits(A_str)
B = str_a_bits(B_str)

# operaciones
suma, carry = sumador_4_bits(A, B)
resta = restador_4_bits(A, B)

# resultados
print("\nResultados:")
print("A     =", bits_a_str(A))
print("B     =", bits_a_str(B))
print("SUMA  =", ('1' if carry else '0') + bits_a_str(suma))
print("RESTA =", bits_a_str(resta))


PRUEBAS 
PRUEBA 1
<img width="1066" height="231" alt="image" src="https://github.com/user-attachments/assets/1ff63af1-a915-448e-b482-f180c15c1814" />
PRUEBA 2 
<img width="1079" height="279" alt="image" src="https://github.com/user-attachments/assets/535736e6-87f6-453b-aaf5-8c5d33d7b03d" />
PRUEBA 3 
<img width="1072" height="311" alt="image" src="https://github.com/user-attachments/assets/fa42331a-9649-43af-a382-dcad24b036b1" />






