# MA2003B-Equipo-5

## Descripción
**VaRAiM** es un framework académico que aplica metodologías de finanzas cuantitativas (Value-at-Risk, GARCH, Teoría de Valor Extremo y simulaciones Monte Carlo) para pronosticar la calidad del aire en la Zona Metropolitana de Monterrey. 

El proyecto nace de la necesidad de superar las limitaciones de los modelos actuales de pronóstico deterministico, que no cuantifican adecuadamente la incertidumbre y riesgo de eventos extremos de contaminación, cruciales para la toma de decisiones en salud pública.

Documentación detallada:
- [Documento principal — VAR_AIRE_MONTERREY]([[./VAR_AIRE_MONTERREY.md](https://github.com/sntsemilio/MA2003B-Equipo-5-VaRaiM/blob/main/VAR_AIRE_MONTERREY.md](https://github.com/sntsemilio/MA2003B-Equipo-5-VaRaiM/blob/main/Referencias/VAR_AIRE_MONTERREY.md)))

## Requisitos Previos

- Python 3.10 o superior
- pip (gestor de paquetes de Python)
- Git

## Configuración del Entorno de Desarrollo

### 1. Clonar el Repositorio

```bash
git clone https://github.com/sntsemilio/MA2003B-Equipo-5.git
cd MA2003B-Equipo-5
```

### 2. Crear un Entorno Virtual

Es recomendable usar un entorno virtual para aislar las dependencias del proyecto:

**En Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**En macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Instalar Dependencias

Una vez activado el entorno virtual, instala las dependencias del proyecto:

```bash
pip install -r requirements.txt
```

### 4. Verificar la Instalación

Para verificar que todas las dependencias se instalaron correctamente:

```bash
pip list
```

## Actualizar Dependencias

Si necesitas agregar nuevas dependencias al proyecto:

1. Instala el paquete necesario:
```bash
pip install nombre-del-paquete
```

2. Actualiza el archivo requirements.txt:
```bash
pip freeze > requirements.txt
```

3. Haz commit de los cambios:
```bash
git add requirements.txt
git commit -m "Actualizar dependencias"
git push
```

## Desactivar el Entorno Virtual

Cuando termines de trabajar, desactiva el entorno virtual:

```bash
deactivate
```

## Estructura del Proyecto

```
MA2003B-Equipo-5/
├── .gitignore
├── requirements.txt
└── README.md
```

## Colaboración

### Flujo de Trabajo

1. Crea una rama para tu funcionalidad:
```bash
git checkout -b feature/nombre-funcionalidad
```

2. Realiza tus cambios y haz commits:
```bash
git add .
git commit -m "Descripción de los cambios"
```

3. Sube tu rama al repositorio:
```bash
git push origin feature/nombre-funcionalidad
```

4. Crea un Pull Request en GitHub para revisión

## Solución de Problemas

### Error al instalar dependencias

Si encuentras errores al instalar las dependencias, intenta:

```bash
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir
```

### Conflictos de versiones

Si hay conflictos con las versiones de Python, verifica tu versión:

```bash
python --version
```

## Contribuidores

- José Emilio Gomez Santos
- Santiago Perez Almazan
- Marcelo Sanchez Rodriguez
- Jose Luis Montibeller Gonzalez
- Jesús Emilio Medina García

## Licencia

MIT License (Modificada)

Copyright (c) 2025 José Emilio Gómez Santos y colaboradores.

Se concede permiso, de manera gratuita, a cualquier persona que obtenga una copia
de este software y los archivos de documentación asociados (el “Software”), para usar
el Software sin restricción, incluyendo, sin limitación, los derechos a usar, copiar y
distribuir el Software, con la condición de que:

1. Cualquier modificación o distribución derivada del Software requiere autorización
   escrita de los autores originales.
2. Debe mantenerse el aviso de copyright y esta nota de permiso en todas las copias.

EL SOFTWARE SE PROPORCIONA “TAL CUAL”, SIN GARANTÍA DE NINGÚN TIPO.
