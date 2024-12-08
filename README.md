# tecnicas-programacion
class Mago:
    def __init__(self, nombre, vida, inteligencia, mana):
        self.nombre = nombre
        self.vida = vida
        self.inteligencia = inteligencia
        self.mana = mana
        self.escudo_activo = False

    def atributos(self):
        print(f"\n{self.nombre} - Atributos:")
        print(f"· Vida: {self.vida}")
        print(f"· Inteligencia: {self.inteligencia}")
        print(f"· Maná: {self.mana}")

    def esta_vivo(self):
        return self.vida > 0

    def atacar_basico(self, enemigo):
        daño = self.inteligencia
        enemigo.vida -= daño
        print(f"{self.nombre} realiza un ataque básico causando {daño} de daño a {enemigo.nombre}")

    def bola_de_fuego(self, enemigo):
        if self.mana >= 10:
            daño = self.inteligencia * 2
            enemigo.vida -= daño
            self.mana -= 10
            print(f"{self.nombre} lanza una Bola de Fuego causando {daño} de daño a {enemigo.nombre}")
        else:
            print(f"{self.nombre} no tiene suficiente maná para Bola de Fuego")

    def curacion(self):
        if self.mana >= 8:
            curacion = 15
            self.vida += curacion
            self.mana -= 8
            print(f"{self.nombre} utiliza Curación y recupera {curacion} puntos de vida")
        else:
            print(f"{self.nombre} no tiene suficiente maná para Curación")

    def escudo_magico(self):
        if self.mana >= 5:
            self.escudo_activo = True
            self.mana -= 5
            print(f"{self.nombre} activa Escudo Mágico y reducirá el daño recibido en el próximo turno")
        else:
            print(f"{self.nombre} no tiene suficiente maná para Escudo Mágico")

    def recibir_ataque(self, daño):
        if self.escudo_activo:
            daño = max(daño - 10, 0)  # Reduce el daño en 10 puntos
            self.escudo_activo = False
        self.vida -= daño
        print(f"{self.nombre} recibe {daño} puntos de daño")

def combate(mago_1, mago_2):
    turno = 1
    while mago_1.esta_vivo() and mago_2.esta_vivo():
        print(f"\n--- Turno {turno} ---")
        print(f">>> Acción de {mago_1.nombre}")
        mago_1.atributos()
        print("(1) Ataque básico (2) Bola de Fuego (3) Curación (4) Escudo Mágico")
        accion = int(input(f"Elige una acción para {mago_1.nombre}: "))
        if accion == 1:
            mago_1.atacar_basico(mago_2)
        elif accion == 2:
            mago_1.bola_de_fuego(mago_2)
        elif accion == 3:
            mago_1.curacion()
        elif accion == 4:
            mago_1.escudo_magico()
        else:
            print("Acción inválida, turno perdido")

        if mago_2.esta_vivo():
            print(f"\n>>> Acción de {mago_2.nombre}")
            mago_2.atributos()
            mago_2.atacar_basico(mago_1)  # Simplemente atacar para simplificar el ejemplo

        turno += 1

    if mago_1.esta_vivo():
        print(f"\n¡{mago_1.nombre} ha ganado!")
    elif mago_2.esta_vivo():
        print(f"\n¡{mago_2.nombre} ha ganado!")
    else:
        print("\n¡Empate!")

# Crear personajes
mago_1 = Mago("Merlín", 100, 15, 50)
mago_2 = Mago("Morgana", 90, 18, 40)

# Iniciar combate
combate(mago_1, mago_2)
