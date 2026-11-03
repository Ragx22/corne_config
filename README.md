# Corne Keymap (QWERTZ, ZMK)

Meine ZMK Config für eine Corne mit **nice!nano v2** und **nice!view** Displays. Genutzt werden 36 Tasten (3 x 5 Spalten pro Seite plus je 3 Daumentasten), die äußeren Spalten der 42-Tasten-Matrix sind ungenutzt.

Das Betriebssystem muss auf **deutschem Tastaturlayout** stehen. ZMK sendet nur HID Codes (US-Positionen), die deutschen Zeichen entstehen erst im Betriebssystem. Deshalb steht in der Keymap für `Z` der Code `Y` und umgekehrt.

## Layer

### 0: Base (QWERTZ)

```
┌───┬───┬───┬───┬───┐       ┌───┬───┬───┬───┬───┐
│ Q │ W │ E │ R │ T │       │ Z │ U │ I │ O │ P │
├───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┤
│ A │ S │ D │ F │ G │       │ H │ J │ K │ L │ Ö │
├───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┤
│ Y │ X │ C │ V │ B │       │ N │ M │ , │ . │ - │
└───┴───┴───┴───┴───┘       └───┴───┴───┴───┴───┘
        ┌─────┬──────────┬───────┐   ┌───────┬──────────┬──────┐
        │ Win │ Space/SYM│ Shift │   │ Enter │ Bksp/NAV │ AltGr│
        └─────┴──────────┴───────┘   └───────┴──────────┴──────┘
```

Die Daumentasten **Space** und **Backspace** sind Layer-Taps: kurz tippen gibt das Zeichen, halten schaltet den Layer **SYM** (links) bzw. **NAV** (rechts).

### 1: SYM (Symbole und Zahlen)

```
┌───┬───┬───┬───┬───┐       ┌───┬───┬───┬───┬───┐
│ ! │ " │ § │ $ │ % │       │ & │ / │ ( │ ) │ = │
├───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┤
│ 1 │ 2 │ 3 │ 4 │ 5 │       │ 6 │ 7 │ 8 │ 9 │ 0 │
├───┼───┼───┼───┼───┤       ├───┼───┼───┼───┼───┤
│ < │ > │ @ │ # │ \ │       │ ? │ [ │ ] │ + │ * │
└───┴───┴───┴───┴───┘       └───┴───┴───┴───┴───┘
        ┌─────┬──────────┬───────┐   ┌───────┬──────────┬──────┐
        │  Ä  │  (trans) │   ß   │   │   Ü   │    |     │  €   │
        └─────┴──────────┴───────┘   └───────┴──────────┴──────┘
```

### 2: NAV (Navigation, Funktionstasten, Bluetooth)

```
┌─────┬─────┬─────┬─────┬─────┐       ┌──────┬──────┬────┬─────┬─────┐
│ F1  │ F2  │ F3  │ F4  │ F5  │       │ PgUp │ Home │ ↑  │ End │ Del │
├─────┼─────┼─────┼─────┼─────┤       ├──────┼──────┼────┼─────┼─────┤
│ F6  │ F7  │ F8  │ F9  │ F10 │       │ PgDn │  ←   │ ↓  │  →  │ Bksp│
├─────┼─────┼─────┼─────┼─────┤       ├──────┼──────┼────┼─────┼─────┤
│ F11 │ F12 │ Tab │ Esc │  -  │       │ Mute │ Vol- │Vol+│ ⏯  │  ~  │
└─────┴─────┴─────┴─────┴─────┘       └──────┴──────┴────┴─────┴─────┘
        ┌───────┬───────┬───────┐   ┌────────┬───────┬───────┐
        │ BT 1  │ BT 2  │ BT 3  │   │ BT clr │   -   │   -   │
        └───────┴───────┴───────┘   └────────┴───────┴───────┘
```

Ein `-` auf den Daumentasten bedeutet **transparent**: die Taste verhält sich wie auf dem Layer darunter.

## Combos

Umlaute und ß sind zusätzlich als Combos auf dem Base Layer erreichbar (zwei Tasten gleichzeitig, 40 ms):

| Zeichen | Tasten |
|---|---|
| Ü | P + Ö |
| Ä | Ö + - |
| ß | O + P |

## Firmware

Fertige Dateien gibt es unter [Releases](../../releases):

| Datei | Zweck |
|---|---|
| `corne_left.uf2` | Linke Hälfte |
| `corne_right.uf2` | Rechte Hälfte |
| `settings_reset.uf2` | Setzt Bluetooth Pairings und Einstellungen zurück |

### Flashen

1. Die Hälfte per USB anschließen und den Reset-Knopf zweimal schnell drücken. Das Board erscheint als Laufwerk (`NICENANO`).
2. Die passende `.uf2` Datei auf das Laufwerk kopieren. Das Board startet danach automatisch neu.
3. Dasselbe mit der anderen Hälfte wiederholen.
4. Bei Verbindungsproblemen zuerst `settings_reset.uf2` auf beide Hälften flashen, danach die normale Firmware erneut.

## Selbst bauen

Die Firmware wird per GitHub Actions gebaut (`.github/workflows/build.yml`). Jeder Push startet einen Build, die Dateien liegen danach als Artefakte am Workflow Lauf. Die Boards und Shields stehen in `build.yaml`, die Keymap in `config/corne.keymap`.
