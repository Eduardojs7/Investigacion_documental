# 📡 Cable FTDI y su Uso en Raspberry Pi

Un **cable FTDI** es un adaptador **USB a serial** basado en el chip **FT232RL** u otro de la familia FTDI. Se usa para comunicar computadoras con dispositivos que tienen una interfaz **UART**, como **microcontroladores** o módulos en una **Raspberry Pi**.

## 🔌 Conexión del cable FTDI a la Raspberry Pi

Los cables FTDI tienen **4 o más pines** para la comunicación serial:

| Cable FTDI | Función        | Raspberry Pi (GPIO)  |
|------------|---------------|----------------------|
| **Negro**  | GND           | GND (Pin 6)         |
| **Blanco** | TXD (Salida)  | RXD (GPIO 15 - Pin 10) |
| **Verde**  | RXD (Entrada) | TXD (GPIO 14 - Pin 8) |

⚠️ **¡No conectes VCC del FTDI a la Raspberry Pi!**  
El FTDI puede operar a **5V o 3.3V**, pero la Raspberry Pi trabaja con **3.3V en sus GPIOs**. Si el FTDI está configurado en **5V**, podría **dañar** la Raspberry Pi. Asegúrate de que el voltaje sea **compatible**.

## 🖥️ Uso con PuTTY en Windows/Linux

1. **Conecta el cable FTDI al PC.**
2. **Verifica el puerto COM asignado:**
   - **Windows:** Abre el **Administrador de dispositivos** y busca el puerto (Ej: `COM3`).
   - **Linux:** Usa el siguiente comando para identificarlo:
     ```bash
     ls /dev/ttyUSB*
     ```
     (Ejemplo de salida: `/dev/ttyUSB0`)
3. **Configura PuTTY:**
   - **Connection type:** Serial  
   - **Serial line:** `COM3` o `/dev/ttyUSB0`  
   - **Speed (baud):** `9600`  
   - **Flow Control:** Ninguno  
4. **Presiona "Open"** y ya puedes enviar o recibir datos desde la Raspberry Pi.

## 🛠️ Uso con `minicom` en Linux

Si prefieres la terminal en Linux, puedes usar `minicom`:

```bash
sudo apt install minicom  # Instalar si no lo tienes
sudo minicom -b 9600 -o -D /dev/ttyUSB0
