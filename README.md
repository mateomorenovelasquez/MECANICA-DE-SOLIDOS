# Invariantes del Tensor de Esfuerzos y Esfuerzos Desviadores en Python

Este repositorio contiene la formulación y el cálculo simbólico de los **invariantes de esfuerzos** (totales, hidrostáticos y desviadores) en 3D utilizando la librería `SymPy` de Python.

## 📌 Contenido del Proyecto

El proyecto desarrollado en los Jupyter Notebooks aborda:

* **Deducción del Polinomio Característico:** Planteamiento del problema de valores propios para el tensor de esfuerzos $3 \times 3$.

* **Cálculo de Invariantes Totales (**$I_1, I_2, I_3$**):** Obtención de los coeficientes del polinomio característico mediante determinantes y operaciones matriciales simbólicas.

* **Tensor de Esfuerzos Hidrostáticos:** Definición a partir del esfuerzo medio ($\sigma_m = \frac{\sigma_x + \sigma_y + \sigma_z}{3}$) y cálculo de sus invariantes ($\tilde{I}_1, \tilde{I}_2, \tilde{I}_3$).

* **Tensor Desviador de Esfuerzos (**$\mathbf{s}$**):** Descomposición del tensor total y cálculo de los invariantes desviadores ($J_1, J_2, J_3$).

* **Demostración de Identidades:** Verificación algebraica de relaciones fundamentales como $J_2 = \frac{1}{3}I_1^2 - I_2$.

## 📐 Fundamento Teórico

### 1. Tensor de Esfuerzos Totales

El tensor de esfuerzos tridimensional se representa en formato matricial como:

$$
\boldsymbol{\sigma} = \begin{bmatrix} \sigma_x & \tau_{xy} & \tau_{xz} \\ \tau_{xy} & \sigma_y & \tau_{yz} \\ \tau_{xz} & \tau_{yz} & \sigma_z \end{bmatrix}
$$

Resolviendo la ecuación característica $\det(\boldsymbol{\sigma} - \sigma_n \mathbf{I}) = 0$, se obtiene el polinomio:

$$
-\sigma_n^3 + I_1 \sigma_n^2 - I_2 \sigma_n + I_3 = 0
$$

Donde los invariantes principales son:

* **Primer Invariante (**$I_1$**):**
  

  $$
  I_1 = \text{tr}(\boldsymbol{\sigma}) = \sigma_x + \sigma_y + \sigma_z
  $$

* **Segundo Invariante (**$I_2$**):**
  

  $$
  I_2 = \sigma_x \sigma_y + \sigma_x \sigma_z + \sigma_y \sigma_z - \tau_{xy}^2 - \tau_{xz}^2 - \tau_{yz}^2
  $$

* **Tercer Invariante (**$I_3$**):**
  

  $$
  I_3 = \det(\boldsymbol{\sigma}) = \sigma_x \sigma_y \sigma_z - \sigma_x \tau_{yz}^2 - \sigma_y \tau_{xz}^2 - \sigma_z \tau_{xy}^2 + 2\tau_{xy}\tau_{xz}\tau_{yz}
  $$

### 2. Componentes Hidrostática y Desviadora

El tensor de esfuerzos se descompone en una parte esférica (hidrostática) y una parte desviadora:

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}_m + \mathbf{s}
$$

* **Esfuerzo Medio (**$\sigma_m$**):**
  

  $$
  \sigma_m = \frac{\sigma_x + \sigma_y + \sigma_z}{3} = \frac{I_1}{3}
  $$

* **Tensor Desviador (**$\mathbf{s}$**):**
  

  $$
  \mathbf{s} = \boldsymbol{\sigma} - \sigma_m \mathbf{I} = \begin{bmatrix} \sigma_x - \sigma_m & \tau_{xy} & \tau_{xz} \\ \tau_{xy} & \sigma_y - \sigma_m & \tau_{yz} \\ \tau_{xz} & \tau_{yz} & \sigma_z - \sigma_m \end{bmatrix}
  $$

Los invariantes del tensor desviador resultan en:

* $J_1 = \text{tr}(\mathbf{s}) = 0$

* $J_2 = \frac{1}{3} I_1^2 - I_2$

## 🚀 Requisitos e Instalación

Para ejecutar los notebooks es necesario instalar las siguientes dependencias de Python:

```
pip install sympy numpy jupyter

```

## 💻 Uso del Código

El repositorio incluye una función basada en traza y determinante para calcular automáticamente los invariantes de cualquier tensor de esfuerzos $3 \times 3$:

```
import sympy as sp

def invariantes(matrix_de_esfuerzos):
    I1 = matrix_de_esfuerzos.trace()
    I2 = (1/2) * (((matrix_de_esfuerzos.trace())**2) - (((matrix_de_esfuerzos)**2).trace()))
    I3 = matrix_de_esfuerzos.det()
    return I1, I2, I3

```

### Ejemplo de Cálculo para el Tensor Desviador

```
import sympy as sp

# Definición de variables simbólicas
sigmax, sigmay, sigmaz = sp.symbols("sigma_x sigma_y sigma_z")
tauxy, tauxz, tauyz = sp.symbols("tau_xy tau_xz tau_yz")

# Esfuerzo medio
sigma_m = (sigmax + sigmay + sigmaz) / 3

# Matriz del tensor desviador
s = sp.Matrix([
    [sigmax - sigma_m, tauxy, tauxz],
    [tauxy, sigmay - sigma_m, tauyz],
    [tauxz, tauyz, sigmaz - sigma_m]
])

# Cálculo de invariantes desviadores J1, J2, J3
J1, J2, J3 = sp.nsimplify(invariantes(s))

```

## 📑 Estructura del Repositorio

* `Invariantes_Esfuerzos_3D.ipynb`: Deducción simbólica del polinomio característico y extracción de los coeficientes de los invariantes $I_1, I_2, I_3$.

* `Esfuerzos_Hidrostaticos_y_Desviadores.ipynb`: Definición del tensor hidrostático, tensor desviador y comprobación simbólica de las expresiones de $J_1, J_2, J_3$.
