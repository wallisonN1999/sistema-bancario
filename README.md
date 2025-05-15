class Cliente:
    def __init__(self, nome, cpf):
        self.nome = nome
        self.cpf = cpf
        self.contas = []

    def adicionar_conta(self, conta):
        self.contas.append(conta)

    def __str__(self):
        return f"{self.nome} (CPF: {self.cpf})"


class Conta:
    def __init__(self, numero, cliente):
        self.numero = numero
        self.cliente = cliente
        self.saldo = 0.0
        self.extrato = []

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            self.extrato.append(f"Depósito: R$ {valor:.2f}")
            print(f"Depósito de R$ {valor:.2f} realizado com sucesso.")
        else:
            print("Valor de depósito inválido.")

    def sacar(self, valor):
        if 0 < valor <= self.saldo:
            self.saldo -= valor
            self.extrato.append(f"Saque: R$ {valor:.2f}")
            print(f"Saque de R$ {valor:.2f} realizado com sucesso.")
        else:
            print("Saldo insuficiente ou valor inválido.")

    def transferir(self, destino, valor):
        if isinstance(destino, Conta) and 0 < valor <= self.saldo:
            self.saldo -= valor
            destino.saldo += valor
            self.extrato.append(f"Transferência para conta {destino.numero}: R$ {valor:.2f}")
            destino.extrato.append(f"Transferência recebida da conta {self.numero}: R$ {valor:.2f}")
            print(f"Transferência de R$ {valor:.2f} realizada para a conta {destino.numero}.")
        else:
            print("Transferência inválida.")

    def mostrar_saldo(self):
        print(f"Saldo atual: R$ {self.saldo:.2f}")

    def mostrar_extrato(self):
        print(f"Extrato da conta {self.numero}:")
        for linha in self.extrato:
            print(" -", linha)
        print(f"Saldo atual: R$ {self.saldo:.2f}")

    def __str__(self):
        return f"Conta {self.numero} - Cliente: {self.cliente.nome}"
