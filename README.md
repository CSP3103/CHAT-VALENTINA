YO VOY HACER LO DE JUGADOR TRATA DE HACER LO ESTADISTICAS TU..... VOY A USAR COMO BASE DE UNA VEZ MI PORYECTO ---- LA VERDAD ESTAMOS NAVEGANDO A CIEGAS YO YA SE QUE HACER CON LO DE JUGADOR ASI QUE ESPERAME Y YO ME ENCARGO DE ESO PORFA OK?
ME MATO
ESTO ES LO QUE HE VENIDO HACIENDOOO:
from sqlmodel import SQLModel, Field, Relationship
from typing import Optional, List
from datetime import datetime
from enum import Enum

# Definir los posibles estados del jugador
class EstadoJugador(str, Enum):
    activo = "Activo"
    inactivo = "Inactivo"
    lesionado = "Lesionado"
    suspendido = "Suspendido"

# Modelo del jugador
class Jugador(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    nombre: str
    edad: int
    numeroUnico: int = Field(ge=1, le=99)  # Limitar a 1-99
    fechaNacimiento: datetime
    nacionalidad: str
    altura: float
    peso: float
    pieDominante: str
    posicion: str  # Cambiar si usas un enum o clase para posición
    estado: EstadoJugador = EstadoJugador.activo
    estadisticas: Optional[str] = None  # Aquí puedes poner estadísticas adicionales si es necesario.

    # Relación si deseas asociar otras tablas, por ejemplo, estadísticas de partidos
    # partidos: List["Partido"] = Relationship(back_populates="jugador")

    # Función para actualizar los datos
    def actualizar_estado(self, estado: EstadoJugador):
        self.estado = estado
