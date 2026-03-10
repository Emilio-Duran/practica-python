*Analista de Machine Learning*

### 1. Resumen del Proyecto y Preparación de Datos

El objetivo principal de este proyecto fue construir un motor predictivo capaz de identificar qué clientes tienen mayor probabilidad de cancelar sus servicios (o dejar calificaciones negativas, como indicador de insatisfacción temprana).

Para lograr esto, preparamos los datos transaccionales actuales y construimos dos modelos distintos. Aplicamos una regla fundamental en el preprocesamiento: la normalización.

Para la Regresión Logística, tuvimos que normalizar los datos numéricos (como el precio y el costo de envío). Como este modelo usa matemáticas para calcular pesos, si no igualamos la escala, el modelo le daría demasiada importancia al precio solo porque el número es más grande que, digamos, la cantidad de cuotas.

Para el Random Forest (Bosque Aleatorio), no usamos normalización. Este modelo funciona haciendo preguntas de "sí o no" en cada paso, así que no se confunde por el tamaño de los números.


### 2. Evaluación de los Modelos

Pusimos a competir a ambos modelos y los evaluamos con datos que no habían visto antes. *Estos fueron los resultados clave:*

*Random Forest:* Logró una Exactitud (Accuracy) del 70%. Es decir, de toda la base de datos, acertó en la mayoría de los casos. Sin embargo, su Recall fue solo del 24%.

*Regresión Logística:* Su Exactitud fue menor (55%), pero su Recall fue mucho mejor: 42%.

##### ¿Qué significa esto para el negocio?

En problemas de cancelación de clientes, la métrica que más nos importa es el Recall. No nos interesa tanto adivinar quién está feliz, sino encontrar a toda costa a los que se quieren ir. En este sentido, la Regresión Logística es la ganadora porque logra identificar a casi la mitad de los clientes en riesgo real, frente a solo una cuarta parte que detecta el Random Forest.

### 3. Análisis Crítico: Underfitting vs. Sesgo

Al analizar por qué los modelos arrojaron estos números, *detectamos dos comportamientos:*

*Underfitting en la Regresión Logística:* El modelo es demasiado "rígido" o simple. Intenta trazar líneas rectas para explicar por qué se enoja un cliente, pero el comportamiento humano rara vez es lineal. Entiende una parte del problema, pero se le escapan muchos matices.

*Sesgo por volumen en el Random Forest:* Aunque controlamos el modelo para que no memorizara los datos (overfitting), el algoritmo se dio cuenta de que la inmensa mayoría de nuestros clientes están felices. Por lo tanto, descubrió que era más "seguro" predecir que nadie va a cancelar. Por eso su exactitud general es alta, pero falla a la hora de encontrar a las minorías insatisfechas.

### 4. Factores que detonan la cancelación

Al abrir la "caja negra" de los modelos para ver en qué se están fijando, descubrimos que los factores que hoy generan más alertas de insatisfacción son netamente financieros:

*Precio total*

*Costo de envío*

*Cantidad de cuotas*

Adicionalmente, el modelo detecta que ciertos vendedores y categorías específicas acumulan un riesgo mucho mayor, lo que apunta a posibles problemas logísticos puntuales.

### 5. Estrategia Propuesta y Próximos Pasos

Basados en estos hallazgos, *proponemos las siguientes acciones inmediatas:*

*Campaña de Retención Preventiva:* Sugiero poner a trabajar el modelo de Regresión Logística de inmediato. Si detecta que un cliente está en riesgo, podemos automatizar el envío de un beneficio de bajo costo (como un cupón de envío gratis en su próxima compra). Aunque el modelo genere algunas alertas falsas, el costo de dar un cupón es infinitamente menor que el costo de perder y tratar de recuperar a un cliente.

*Transparencia de costos:* Dado que las cuotas y los costos de envío son detonantes, debemos revisar cómo comunicamos estos cargos extra antes del pago para evitar fricciones.

*Evolución de los Datos:* El modelo nos está diciendo claramente que los datos actuales (qué compró y cómo pagó) solo explican una parte del problema. Para que el modelo pase de un 42% a un 80% de efectividad, el equipo de datos necesita empezar a registrar variables de experiencia de usuario: tiempo real de entrega, contactos con soporte técnico y devoluciones.