
# 🔧 GUÍA DEFINITIVA: Cómo medir transistores con multímetro

> **Nota inicial:** Usar multímetro en **escala de diodos** (🔊 con pitido).  
> **Valores típicos:** 0.4V a 0.7V = sano | OL = abierto | 0.000V = corto

---

## 1. MOSFET (Canal N y Canal P)

### 🔷 MOSFET Canal N

| Medición | Resultado esperado |
|----------|---------------------|
| D(+) S(-) | 0.4V - 0.7V |
| S(+) D(-) | OL |
| **Activación:** G(+) S(-) (tocar 1 seg) | — |
| Post-activación: D(+) S(-) | Continuidad (0.000V) |
| Post-activación: S(+) D(-) | Continuidad (0.000V) |

### 🔴 MOSFET Canal P

| Medición | Resultado esperado |
|----------|---------------------|
| D(+) S(-) | OL |
| S(+) D(-) | 0.4V - 0.7V |
| **Activación:** G(-) S(+) (tocar 1 seg) | — |
| Post-activación: D(+) S(-) | Continuidad (0.000V) |
| Post-activación: S(+) D(-) | Continuidad (0.000V) |

### 📌 Tips y observaciones para MOSFET

- **Desactivar:** tocar G con S (destornillador o pinza) después de cada prueba.
- **Cuidado:** los dedos pueden activar/desactivar por capacitancia.
- **Sano:** solo conduce después de tocar la compuerta.
- **Dañado:** corto D-S sin activar, o no conduce después de activar.
- Los MOSFET de potencia tienen diodo de cuerpo → por eso da 0.4V-0.7V en un sentido.

---

## 2. BJT (NPN y PNP)

> **Los BJT NO se activan tocando.** Se miden como dos diodos (Base-Emisor y Base-Colector).

### 🔷 BJT NPN

| Medición | Resultado esperado |
|----------|---------------------|
| B(+) E(-) | 0.5V - 0.7V |
| B(+) C(-) | 0.5V - 0.7V |
| B(-) E(+) | OL |
| B(-) C(+) | OL |
| C(+) E(-) | OL |
| C(-) E(+) | OL |

### 🔴 BJT PNP

| Medición | Resultado esperado |
|----------|---------------------|
| B(-) E(+) | 0.5V - 0.7V |
| B(-) C(+) | 0.5V - 0.7V |
| B(+) E(-) | OL |
| B(+) C(-) | OL |
| C(+) E(-) | OL |
| C(-) E(+) | OL |

### 📌 Tips y observaciones para BJT

- **Identificar Base:** la pata que da voltaje con las otras dos es la Base.
- **Identificar tipo:** si Base(+) da con las otras → NPN. Si Base(-) da → PNP.
- **Recordatorio fácil:** la flecha del emisor indica polaridad (NPN = flecha sale → B+ da con E).
- **hFE:** si tu multímetro tiene conector, podés medir ganancia (50-800).
- **Dañado:** corto C-E sin importar polaridad, o diodos rotos.

---

## 3. IGBT (Canal N y Canal P)

> **Se miden IGUAL que los MOSFET.** Misma lógica, distintos nombres de patas (C=Colector, E=Emisor, G=Compuerta).

### 🔷 IGBT Canal N

| Medición | Resultado esperado |
|----------|---------------------|
| C(+) E(-) | 0.4V - 0.7V |
| E(+) C(-) | OL |
| **Activación:** G(+) E(-) (tocar 1 seg) | — |
| Post-activación: C(+) E(-) | Continuidad (0.000V) |
| Post-activación: E(+) C(-) | Continuidad (0.000V) |

### 🔴 IGBT Canal P

| Medición | Resultado esperado |
|----------|---------------------|
| C(+) E(-) | OL |
| E(+) C(-) | 0.4V - 0.7V |
| **Activación:** G(-) E(+) (tocar 1 seg) | — |
| Post-activación: C(+) E(-) | Continuidad (0.000V) |
| Post-activación: E(+) C(-) | Continuidad (0.000V) |

### 📌 Tips y observaciones para IGBT

- **No midas G-E como BJT** → la compuerta es aislada, debe dar OL.
- **Algunos IGBT tienen:** diodo Zener interno G-E (protección) o resistencia G-E (10kΩ-50kΩ).
- **Desactivar:** igual que MOSFET, tocar G con E.
- **Diodo C-E:** puede dar 0.3V a 1.2V según el tipo (rápido o lento).
- **Confusión común:** C y E no son D y S, pero la medición es idéntica.

---

## 📊 TABLA RESUMEN COMPARATIVA

| Tipo | Diferencia clave | Activación | Post-activación |
|------|------------------|------------|------------------|
| **MOSFET** | Diodo D-S | Tocar G-S | Corto D-S |
| **BJT** | Dos diodos B-E / B-C | No aplica | No aplica |
| **IGBT** | Diodo C-E | Tocar G-E | Corto C-E |

---

## ⚠️ NOTAS GENERALES IMPORTANTES (LEER SIEMPRE)

1. **Siempre descargar:** tocar G con S (o G con E en IGBT) antes de medir.
2. **Valores sospechosos:** 0.000V sin activar = corto. OL después de activar = abierto.
3. **Multímetro:** usar siempre escala de diodos (la del símbolo ▶+). La escala de resistencia puede dar lecturas raras por voltaje bajo.
4. **Identificar patas sin datasheet:**
   - MOSFET/IGBT: la pata aislada (que da OL con todas) es la compuerta (G).
   - BJT: la pata que da voltaje con las otras dos es la Base (B).
5. **Si todo da OL:** revisá puntas del multímetro o fijate si el transistor es Darlington (puede dar 0.8V-1.2V).
6. **Componente en placa:** puede dar lecturas falsas por otros componentes conectados. Mejor medir fuera del circuito.

---

## 🧠 TRUCO RÁPIDO PARA RECORDAR

```
MOSFET = Diodo + Toque
BJT    = Dos diodos (sin toque)
IGBT   = Diodo + Toque (como MOSFET)
```

**NPN vs PNP (BJT):**
- NPN: Base POSITIVA conduce con E y C
- PNP: Base NEGATIVA conduce con E y C

**Canal N vs Canal P (MOSFET/IGBT):**
- Canal N: Diodo D→S (o C→E) + G POSITIVA activa
- Canal P: Diodo S→D (o E→C) + G NEGATIVA activa

---

✅ **Listo. Esto reemplaza todas tus notas anteriores.**  
¿Necesitás que le agregue algo más? (ej: fotos, diagramas ASCII, o algún otro componente como JFET)