---
title: "Resoluciones Web - Como hacerlo fácil"
description: ""
tags: ["resoluciones", "web", "userscript"]
draft: false
date: 2025-03-03
---

## ¿Por qué es tan dificil?


Básicamente porque te engaña. Pone una fecha por defecto y la misma no es valida, es la fecha del día. Yo entiendo que lo ponen de esa manera para no sobrecargar la búsqueda. Pero la sobrecarga aún más si consideramos que uno debe repetir un y otra vez la misma busqueda.

## Solución no general.

Yo uso el siguiente userscripts en [Tampermokey](https://www.tampermonkey.net/) que me arregla el problema.

Si no conoces algo de [Tampermonkey](https://www.tampermonkey.net/), por favor no lo uses.

Básicaente fija la fecha por defecto en 5 años atras asi no perdemos un año en hacer una.

```js
// ==UserScript==
// @name         Corregir Formulario Hostil
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Corrige campos incorrectos automáticamente
// @author       Roberto Insfrán
// @match        https://www.csj.gov.py/ResolucionesWeb/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Función para obtener la fecha actual en formato DD/MM/YYYY
    function obtenerFechaActual() {
        const hoy = new Date();
        const dia = String(hoy.getDate()).padStart(2, '0');
        const mes = String(hoy.getMonth() + 1).padStart(2, '0');
        const anio = hoy.getFullYear();
        return `${dia}/${mes}/${anio}`;
    }

    // Establece la fecha de 5 años atrás
    function obtenerFechaHace5Anos() {
        const hoy = new Date();
        hoy.setFullYear(hoy.getFullYear() - 5);
        const dia = String(hoy.getDate()).padStart(2, '0');
        const mes = String(hoy.getMonth() + 1).padStart(2, '0');
        const anio = hoy.getFullYear();
        return `${dia}/${mes}/${anio}`;
    }

    // Establece la fecha de hace 5 años en el campo
    document.getElementById("MainContent_datepickerDesde").value = obtenerFechaHace5Anos();

    // Agrega el evento de envío del formulario
    document.querySelector("form").addEventListener("submit", function(e) {
        if (document.getElementById("MainContent_datepickerDesde").value === obtenerFechaActual()) {
            alert("Corrige los datos. La fecha no puede ser la actual.");
            e.preventDefault();
        }
    });
})();

```

{{< graphcomment >}}
















------
