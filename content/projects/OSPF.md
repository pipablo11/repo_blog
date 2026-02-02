---
title: "Protocolo OSPF: Estudio e implementación en MikroTiK"
date: 2026-01-29
description: "Análisis técnico, configuración y simulación de escenarios de enrutamiento dinámico OSPFv2 utilizando routers MikroTik RouterOS v7."
tags: ["mikrotik", "ospf", "pnetLab", "proxmox", "wireshark", "winbox"]
categories: ["proyectos", "laboratorio"]
showTableOfContents: true
showAuthor: true
layout: "simple"
featureImage: "" # Puedes añadir una ruta a una imagen aquí: "img/ospf-cover.jpg"
---

En este proyecto he realizado un análisis exhaustivo y una implementación práctica del protocolo de enrutamiento dinámico **OSPF (Open Shortest Path First)**. El objetivo principal ha sido comprender cómo este estándar abierto utiliza el algoritmo de Dijkstra para calcular rutas eficientes y adaptarse automáticamente a cambios en la topología de red.

El trabajo abarca desde los fundamentos teóricos (LSDB, mensajes LSA y jerarquía de áreas) hasta la configuración avanzada en equipos de red reales virtualizados.

## 🛠️ Tecnologías Utilizadas

Para llevar a cabo la prueba de concepto y las simulaciones, se ha desplegado un entorno de laboratorio utilizando las siguientes herramientas:

* **Virtualización:** **PNetLab** corriendo sobre un hipervisor **Proxmox**.
* **Enrutamiento:** Routers virtuales **MikroTik** con sistema operativo **RouterOS v7** (versión 7.21.1).
* **Gestión:** Configuración realizada mediante **Winbox**.
* **Análisis de Red:** **Wireshark** para la captura y análisis de paquetes a bajo nivel.


## 🚀 Escenarios Implementados

El proyecto se ha dividido en dos grandes simulaciones para probar distintas capacidades del protocolo:

### 1. Topología con Redundancia
Se diseñó una red con 4 routers formando un ciclo para verificar la resiliencia del protocolo.

* **Objetivo:** Comprobar cómo OSPF actualiza las rutas ante fallos o cambios de métricas.
* **Pruebas:** Se simuló la caída de un router y el aumento de costes en los enlaces. Mediante **traceroute**, se verificó que el tráfico cambiaba de ruta automáticamente para evitar el nodo caído o el enlace costoso.
* **Resultado:** Se observó la importancia de ajustar correctamente los tiempos de *hello interval* y *dead interval* para equilibrar la velocidad de convergencia y la carga de tráfico en la red.

### 2. Segmentación Multi-Área
Se simuló una estructura corporativa dividida en zonas lógicas para mejorar la organización y gestión.

* **Estructura:**
    * **Área Backbone (0.0.0.0):** Núcleo de la red que conecta las sucursales.
    * **Área A y Área B:** Sucursales independientes con sus propias subredes LAN.
* **Configuración:** Se configuraron routers de frontera (ABR) para gestionar el intercambio de rutas entre el backbone y las áreas periféricas.

## 🔒 Securización de la Red

Un aspecto crítico del proyecto fue la seguridad. Se implementaron mecanismos de autenticación para evitar que routers no autorizados se unieran a la topología.

Se configuraron plantillas de interfaz (*Interface Templates*) con autenticación criptográfica **MD5**, demostrando una mayor seguridad frente al uso de contraseñas en texto plano (*Simple password*).

## 📡 Análisis de Tráfico

Utilizando **Wireshark**, se capturó el tráfico en las interfaces para diseccionar el funcionamiento interno de OSPF. Se identificaron y analizaron los siguientes tipos de paquetes:

* **Paquetes Hello:** Para el descubrimiento de vecinos y mantenimiento de la conexión (keepalive).
* **DB Description y LS Update:** Para la sincronización de la base de datos de estado de enlace (LSDB) entre routers.

## 📝 Documentación Completa

Si quieres ver el detalle de las configuraciones, las tablas de enrutamiento y las capturas completas, puedes descargar la memoria del proyecto aquí:

{{< button href="/docs/SCO-OSPF(1).pdf" target="_blank" >}}
  Descargar PDF del Proyecto
{{< /button >}}
