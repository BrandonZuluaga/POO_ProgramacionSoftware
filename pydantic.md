# Pydantic: Validación y Modelado de Datos en Python

# ¿Qué es Pydantic?

Pydantic es una librería de Python diseñada para: - **Validar datos**:
Verificar que los datos cumplan los tipos esperados. - **Parsear
datos**: Convertir datos de entrada (ej. JSON, dict) en objetos Python
tipados. - **Definir modelos de datos**: Crear clases claras y seguras
usando *type hints*.

Se basa en las anotaciones de tipo de Python e integra valores por
defecto, validaciones automáticas y conversión de tipos.

------------------------------------------------------------------------

## Instalación

``` bash
pip install pydantic
```

------------------------------------------------------------------------

## Ejemplo Básico

``` python
from pydantic import BaseModel

class Usuario(BaseModel):
    id: int
    nombre: str
    activo: bool = True  # valor por defecto

data = {"id": "123", "nombre": "Brandon"}
usuario = Usuario(**data)

print(usuario)
print(usuario.id)        # 123 (convertido automáticamente a int)
print(usuario.activo)    # True
```

Convierte `"123"` a `123` (int).\
Rellena `activo` con el valor por defecto.\
Lanza errores si faltan campos obligatorios o si los tipos son
inválidos.

------------------------------------------------------------------------

## Validaciones Avanzadas

``` python
from pydantic import BaseModel, EmailStr, Field

class Cliente(BaseModel):
    email: EmailStr
    edad: int = Field(..., ge=18, le=99)  # entre 18 y 99 años

cliente = Cliente(email="correo@ejemplo.com", edad=25)
print(cliente)
```

Reglas: - `EmailStr` valida que el correo tenga formato correcto. -
`Field(..., ge=18, le=99)` fuerza que la edad esté entre 18 y 99.

------------------------------------------------------------------------

## Ejemplo con FastAPI

FastAPI usa Pydantic para manejar validaciones automáticamente:

``` python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    nombre: str
    precio: float
    disponible: bool = True

@app.post("/items/")
def crear_item(item: Item):
    return item
```

Cuando se hace un POST con un JSON, Pydantic valida los datos y devuelve
un error detallado si no cumplen.

------------------------------------------------------------------------

## Beneficios de Pydantic

-   Código **más seguro** y **legible**.
-   Validaciones automáticas sin lógica extra.
-   Conversión de tipos transparente.
-   Integración perfecta con **FastAPI**, **SQLModel** y otros
    frameworks modernos.

------------------------------------------------------------------------

## Nota sobre la Versión 2

En 2023 se lanzó **Pydantic v2** con: - Mejoras de rendimiento (hasta
10x más rápido). - API más consistente. - Algunas diferencias con la v1
en validaciones y configuración.

------------------------------------------------------------------------

## Conclusión

Pydantic es la herramienta estándar en Python para trabajar con datos
estructurados de forma: - **Sencilla** - **Segura** - **Eficiente**

Ideal para proyectos con APIs, validaciones de entrada y modelado de
datos.
