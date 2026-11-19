<p align="center"><img src="logo-claro.png" alt="Acopio — gestión de inventario" width="320"></p>

# Branding: Acopio

**Acopio**, gestión de inventario. El proyecto antes se llamaba *StockAPI Manager*.

## Archivos

| Archivo | Uso |
|---|---|
| `isotipo.svg` / `isotipo-oscuro.svg` | Solo el símbolo (fondos claros / oscuros) |
| `logo-claro.svg` / `logo-oscuro.svg` | Isotipo + "Acopio" + subtítulo, horizontal |
| `favicon.svg` | Favicon; cambia de colores solo con `prefers-color-scheme` |
| `favicon-32.png` | Favicon para navegadores viejos |
| `apple-touch-icon.png` | Ícono de iOS, 180×180, fondo `#F6F7F2` (iOS no respeta la transparencia) |
| `logo-claro.png` / `logo-oscuro.png` | README, LinkedIn y slides (exportados a 2x, fondo transparente) |
| `tokens.css` | Variables CSS de la paleta (`--acopio-*`), en claro y oscuro |

El texto de los logos SVG está convertido a trazados (Inter 600 / 400), así que se ve igual aunque la fuente no esté instalada. "Acopio" va con tracking -0.5.

## Paleta

| Token | Variable | Claro | Oscuro |
|---|---|---|---|
| Primario | `--acopio-primary` | `#3D5A2C` | `#7FA05A` |
| Primario hover | `--acopio-primary-hover` | `#324A24` | `#93B36C` |
| Acento | `--acopio-accent` | `#9CBF6E` | `#C5DDA0` |
| Texto | `--acopio-text` | `#1F261B` | `#EEF0E8` |
| Fondo | `--acopio-bg` | `#F6F7F2` | `#1B2018` |
| Superficie | `--acopio-surface` | `#FFFFFF` | `#252B21` |
| Borde | `--acopio-border` | `#D9DCCF` | `#3B4434` |
| Texto secundario | `--acopio-text-secondary` | `#6B6E66` | `#A6AD9F` |

### Estados

| Estado | Variables | Claro (texto / fondo) | Oscuro (texto / fondo) |
|---|---|---|---|
| Éxito | `--acopio-success(-bg)` | `#1F6B3A` / `#E7F4EA` | `#6FCF8E` / `rgba(31,107,58,.22)` |
| Atención | `--acopio-warning(-bg)` | `#8A5A0A` / `#FCF3DF` | `#E8B65A` / `rgba(138,90,10,.24)` |
| Error | `--acopio-error(-bg)` | `#A1261B` / `#FCEBE9` | `#F08A7E` / `rgba(161,38,27,.24)` |

## Reglas de uso

- El verde va solo en acciones y selección, nunca para indicar un estado. Para "éxito" se usa el verde de estado (`#1F6B3A`), no el de marca.
- Un solo botón primario por pantalla.
- Nada de colores hardcodeados en los componentes: siempre variables.
- Dejá aire alrededor del logo: como mínimo, el ancho de un bloque del isotipo.
- No cambies los colores del isotipo ni le agregues sombras.
