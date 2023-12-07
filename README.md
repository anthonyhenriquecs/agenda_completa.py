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
class ListaUnica:
    def __init__(self, elem_class):
        self.lista = []
        self.elem_class = elem_class
    def __len__(self):
        return len(self.lista)
    def __iter__(self):
        return iter(self.lista)
    def __getitem__(self, p):
        return self.lista[p]
    def indindiceValido(self,i):
        return i >= 0 and i < len(self.lista)
    def adiciona(self, elem):
        if self.pesquisa(elem) == 1:
            self.lista.append(elem)
    def remove(self,elem):
        self.lista.remove(elem)
    def pesquisa(self, elem):
        self.verifica_tipo(elem)
        try:
            return self.lista.index(elem)
        except ValueError:
            return -1
    def verifica_tipo(self,elem):
        if not isinstance(elem,self.elem_class):
            raise TypeError("Tipo invalido")
    def ordena(self, chave=None):
        self.lista.sort(key=chave)
@total_ordering
class Nome:
    def __init__(self, nome):
        self.nome = nome
    def __str__(self):
        return self.nome
    def __repr__(self):
        return f"<Classe {type(self).__name__} em 0x{id(self):x} Nome: {self.__nome} Chave: {self.__chave}>"
    def __eq__(self, outro):
        return self.nome == outro.nome
    def __lt__(self, outro):
        return self.nome < outro.nome
    @property
    def nome(self):
        return self.__nome
    @nome.setter
    def nome(self, valor):
        if valor is None or not valor.strip():
            raise ValueError("Nome não pode ser nulo nem em branco")
        self.__nome = valor
        self.__chave = Nome.CriaChave(valor)
    @property
    def chave(self):
        return self.__chave
    @staticmethod
    def CriaChave(nome):
        return nome.strip().lower()
@total_ordering
class TipoTelefone:
    def __init__(self, tipo):
        self.tipo = tipo
    def __str__(self):
        return f"({self.tipo})"
    def __eq__(self, outro):
        if outro is None:
            return False
        return self.tipo == outro.tipo
    def __lt__(self, outro):
        return self.tipo < outro.tipo
