# Node-RED Relay Control (pirelay v2, RELAY1 GPIO 19)

Aquest projecte mostra com controlar el RELAY1 del relay HAT PiRelay v2 de SB Components mitjançant Node-RED i un dashboard web.

## Hardware
- Raspberry Pi (qualsevol model compatible amb GPIO)
- PiRelay v2 (SB Components)
- RELAY1 connectat a GPIO 19 (Pin 35)

## Flow

1. **Switch Dashboard**: permet activar/desactivar el RELAY1 des de la web.
2. **Sortida GPIO**: activa o desactiva el RELAY1 a través del pin GPIO 19.

## Instal·lació

1. Importa el fitxer `flow.json` a Node-RED (`Menú > Importa > Porta-retalls`).
2. Instal·la el node `node-red-dashboard` (si no el tens).
3. Instal·la el node `node-red-node-pi-gpio` (per Raspberry Pi).
4. Connecta el PiRelay v2 a la Raspberry Pi. Comprova que el RELAY1 està associat al GPIO 19 (Pin 35).
5. Accedeix al dashboard: `http://<ip-raspberry>:1880/ui`

## Ús

- Des del dashboard web pots activar o desactivar el RELAY1 fent servir el switch.
- Pots programar l'activació des de Node-RED afegint altres nodes segons necessitats.

## Troubleshooting

- Si el relay no respon, comprova la connexió física i que el GPIO 19 no estigui sent utilitzat per altres processos.
- Comprova permisos d'accés als GPIO (`sudo node-red` per provar).
- Consulta la documentació de PiRelay v2 de SB Components.

---

**Per dubtes o millores, obre una issue al repositori!**