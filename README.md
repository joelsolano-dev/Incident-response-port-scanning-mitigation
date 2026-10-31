Incident Response Report: Unauthorized Network Reconnaissance & Port Scanning
Overview del Incidente
Se detectó una actividad anómala de reconocimiento dentro de la red corporativa. Un actor no autorizado ejecutó un escaneo activo de puertos (Port Scanning) contra un activo de infraestructura crítico, buscando identificar servicios expuestos para eventuales fases de explotación. El equipo de respuesta a incidentes (SOC Tier 1) activó el protocolo de contención perimetral, análisis de trazas de red y auditoría post-mitigación bajo el marco de referencia MITRE ATT&CK (T1595 - Active Scanning).

Paso 1: Detección y Triaje
Durante el monitoreo en tiempo real de la interfaz de red principal (eth0), los sensores del SOC registraron un incremento abrupto de paquetes TCP con bandera SYN provenientes de una fuente externa. El tráfico fue aislado mediante inspección de paquetes en capa 4 para confirmar la presencia de un sondeo masivo de puertos.

<img width="852" height="216" alt="Captura de pantalla 2026-10-30 205643" src="https://github.com/user-attachments/assets/13eb8b77-21b5-4722-bf4a-7f2269d436aa" />


Paso 2: Análisis de Indicadores de Compromiso (IoCs) y Métricas
Se realizó la extracción y correlación forense de los datos capturados para determinar el alcance y vector del ataque:

IP de Origen (Hostil): 127.0.0.1

Táctica y Técnica MITRE ATT&CK: Reconnaissance / Active Scanning (T1595)

Firma de Tráfico: Ráfaga de paquetes TCP SYN sin completar el apretón de manos (Half-Open Scanning)

Impacto y Alcance: Barrido secuencial de 1,000 puertos ejecutado en 0.17 - 0.22 segundos, logrando identificar el servicio SSH activo en el puerto 22/tcp.

Paso 3: Contención y Mitigación
Con el fin de detener la recolección de inteligencia del atacante y prevenir intentos secundarios de fuerza bruta, se aplicó una regla de contención inmediata en el firewall perimetral (UFW) para descartar (DROP) todo el tráfico proveniente de la dirección IP identificada.

Bash
sudo ufw deny from 127.0.0.1 to any
<img width="778" height="358" alt="Captura de pantalla 2026-10-30 205659" src="https://github.com/user-attachments/assets/b6a08c71-ffca-4942-ac5c-7961ee54b5b6" />


Paso 4: Verificación y Auditoría Post-Mitigación
Se ejecutó un escaneo de prueba post-incidente desde la dirección bloqueada para validar la efectividad de la política de seguridad. Telemetría confirmó que los paquetes de sondeo son descartados silenciosamente por el firewall, neutralizando con éxito el vector de reconocimiento y cerrando la fase de respuesta.

<img width="593" height="187" alt="Captura de pantalla 2026-10-30 205908" src="https://github.com/user-attachments/assets/d7ec1b5d-6bdc-4ae5-a5a6-ced2d138cdc9" />
