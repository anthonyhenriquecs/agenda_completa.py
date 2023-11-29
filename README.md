# agenda_completa.py

import sys
import pickle
from functools import total_ordering
def nulo_ou_vazio(texto):
    return texto is None or not texto.strip()
def valida_faixa_inteiro(pergunta, inicio, fim, padrao=None):
    while True:
        try:
            entrada = input(pergunta)
            if nulo_ou_vazio(entrada) and padrao is not None:
                entrada = padrao
            valor = int(entrada)
            if inicio <= valor <= fim:
                return valor
        except ValueError:
            print(f"Valor invalido, favor digitar entre {inicio} e {fim}")
