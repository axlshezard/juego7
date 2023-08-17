# juego7

import random
#dividi bien las clases, las encapsule
class Carta:
    def __init__(self, nombre, valor):
        self.nombre = nombre
        self.valor = valor

class Jugador:
    def __init__(self, nombre, humano=True):
        self.nombre = nombre
        self.mano = []
        self.puntos = 0
        self.plantar = False
        self.humano = humano
#dividi las funciones para hacer el codigo mas modular
def crear_mazo():
    cartas = [
        ("As♠", 1), ("2♠", 2), ("3♠", 3), ("4♠", 4), ("5♠", 5), ("6♠", 6),
        ("7♠", 7), ("10♠", 0.5), ("11♠", 0.5), ("12♠", 0.5),
        ("As♡", 1), ("2♡", 2), ("3♡", 3), ("4♡", 4), ("5♡", 5), ("6♡", 6),
        ("7♡", 7), ("10♡", 0.5), ("11♡", 0.5), ("12♡", 0.5),
        ("As♢", 1), ("2♢", 2), ("3♢", 3), ("4♢", 4), ("5♢", 5), ("6♢", 6),
        ("7♢", 7), ("10♢", 0.5), ("11♢", 0.5), ("12♢", 0.5),
        ("As♣", 1), ("2♣", 2), ("3♣", 3), ("4♣", 4), ("5♣", 5), ("6♣", 6),
        ("7♣", 7), ("10♣", 0.5), ("11♣", 0.5), ("12♣", 0.5)
    ]
    mazo_b = []
    while cartas:
        nombre, valor = cartas.pop(random.randint(0, len(cartas) - 1))
        mazo_b.append(Carta(nombre, valor))
    return mazo_b

def jugar_siete_y_medio():
    mazo = crear_mazo()
    
    j1 = Jugador('Gerardo', True)
    j2 = Jugador('Cristian', True)
    
    j1.mano.append(mazo.pop())
    j2.mano.append(mazo.pop())
    
    while not (j1.plantar and j2.plantar):
        if not j1.plantar:
            mostrar_mano(j1)
            j1.plantar = True if input(f"{j1.nombre} ¿Quieres plantarte? si/no: ").lower() == "si" else j1.plantar
            if not j1.plantar:
                j1.mano.append(mazo.pop())
                input("Presiona Enter para continuar...")
        if not j2.plantar:
            mostrar_mano(j2)
            j2.plantar = True if input(f"{j2.nombre} ¿Quieres plantarte? si/no: ").lower() == "si" else j2.plantar
            if not j2.plantar:
                j2.mano.append(mazo.pop())
                input("Presiona Enter para continuar...")
    #use listas para calcular  los puntajes
    p1 = sum([carta.valor for carta in j1.mano])
    p2 = sum([carta.valor for carta in j2.mano])
    
    p1_7_5 = p1 > 7.5
    p2_7_5 = p2 > 7.5
    
    if p1_7_5 and p2_7_5:
        print("Ambos jugadores pierden.")
    elif p1_7_5:
        print(f"Gana {j2.nombre}")
    elif p2_7_5:
        print(f"Gana {j1.nombre}")
    elif p1 == p2:
        print("Empate")
    elif p1 > p2:
        print(f"Gana {j1.nombre}")
    else:
        print(f"Gana {j2.nombre}")

def mostrar_mano(jugador):
    print(f"Cartas de {jugador.nombre}:")
    for carta in jugador.mano:
        print(f"- {carta.nombre}")
    print(f"Puntos: {sum([carta.valor for carta in jugador.mano])}\n")

if __name__ == "__main__":
    jugar_siete_y_medio()
