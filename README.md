# Node-RED Relay Control per Venus OS amb PiRelay v2 (RELAY1 GPIO 19)

Aquest projecte mostra com controlar el RELAY1 del PiRelay v2 de SB Components a una Raspberry Pi amb Venus OS, utilitzant Node-RED i la utilitat rpigpiosetup.

## Hardware

- Raspberry Pi amb Venus OS (Victron)
- PiRelay v2 (SB Components)
- RELAY1 connectat a GPIO 19 (Pin físic 35)

## Funcionament

La integració funciona gràcies al script [`rpigpiosetup`](https://github.com/kwindrem/RpiGpioSetup), que és l’única via compatible per controlar els GPIO dins Venus OS. El flow de Node-RED no utilitza el node `rpi-gpio out` sinó que executa directament la comanda via un node `exec`.

## Instal·lació

1. **Instal·la Node-RED i el node-red-dashboard** si no ho tens ja.
2. **Assegura’t que Venus OS té la utilitat rpigpiosetup** instal·lada a `/data/etc/rpigpiosetup`.
3. **Importa el fitxer `flow.json` a Node-RED** (`Menú > Importa > Porta-retalls`).
4. **Accedeix al dashboard:** `http://<ip-raspberry>:1880/ui`
5. **Prem el switch RELAY1** per activar o desactivar el relé des del dashboard.

## Detalls tècnics del flow

- El node switch envia “1” (activa) o “0” (desactiva).
- El node function genera la comanda `/data/etc/rpigpiosetup set 19 1` o `/data/etc/rpigpiosetup set 19 0`.
- El node exec executa la comanda directament a Venus OS.

> **Nota:** Si la ruta del script no és `/data/etc/rpigpiosetup`, adapta-la al teu sistema.

## Per què no funcionen els nodes GPIO estàndard?

Venus OS bloqueja l’accés directe als GPIO per garantir la seguretat i consistència del sistema. Només rpigpiosetup (i la pròpia stack Venus OS) poden controlar-los correctament. Els nodes `rpi-gpio out` de Node-RED **no funcionen** en aquest entorn.

## Troubleshooting

- Si el relé no respon des de Node-RED però sí des de Venus OS, comprova la ruta del script i permisos d’execució.
- Executa manualment: `/data/etc/rpigpiosetup set 19 1` i `/data/etc/rpigpiosetup set 19 0` per provar.
- Si tens errors de permisos, potser cal configurar Node-RED per executar-se amb més privilegis.

---

**Per qualsevol dubte o millora, obre una issue al repositori!**