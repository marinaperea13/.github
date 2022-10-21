# TAL.IA: TrAducción de la Lengua de signos mediante Inteligencia Artificial

## Estado del proyecto
- README en desarrollo, pero ya con algo de contenido que mostrar.
- Repositorios auxiliares prácticamente vacíos.

**Here are some ideas to get you started:**

- 🙋‍♀️ A short introduction - what is your organization all about?
- 🌈 Contribution guidelines - how can the community get involved?
- 👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
- 🍿 Fun facts - what does your team eat for breakfast?
- 🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

## Explicacion del objetivo del código (data augmentation + DeepFakes) 

Referencias:
* [*Data augmentation*](https://tal-ia.github.io/data_augmentation/)
* [*DeepFakes*](https://tal-ia.github.io/deepfakes/)

## Origen y obtención de los vídeos (enlace a SACU)

* [Glosario en Lengua de Signos Española](https://sacu.us.es/spp-prestaciones-discapacidad-glosario-pintura).

## Pequeña tabla con resultados de subconjuntos (entrenamiento con datos originales, datos sinteticos, datos originales+sinteticos)

### SACU-I3D-10

Este conjunto se ha creado con **8 clases** tomadas de las palabras del SACU, a saber: alcazar, desierto, blog, apagar, error, fe, cementerio, obispo. Las palabras han sido escogidas al ser comunes y poder encontrarse en otros diccionarios. De hecho, para poder trabajar con un conjunto de datos un poco más complejo, hemos añadido 7 vídeos adicionales del diccionario Spread the Sign, y 8 del Dilse, con la idea de poder usar un conjunto test novedoso.

Para poder poner a prueba nuestra hipótesis —la utilidad de la expansión de datos (*data augmentation*) y de los *deepfakes* para mejorar la precisión de un modelo— optamos por realizar un número considerable de experimentos recurriendo a este conjunto, contemplando en cada caso diferentes configuraciones para obtener información útil. Adicionalmente, cabe destacar que recurrimos al modelo I3D de reconocimiento del lenguaje de signos, tal y como es empleado en el artículo de presentación del conjunto de datos WLASL, *WLASL-LEX: a Dataset for Recognising Phonological Properties in American Sign Language*.

Usamos $S$ para denotar al conjunto de los 10 vídeos originales con los que trabajamos —$S_{I}$ representará a los signantes identificados por $I$ de $S$—, $T_1$ y $T_2$ para las transformaciones, $DF$ para los *DeepFakes*, y D para el conjunto test, formado por 8 vídeos del diccionario Dilse:

$$T_1 = ("aff", "apepper", "blur", "usample-0.1")$$
$$T_2 = ("aff", "bsalt", "mblur", "dsample-0.2")$$

| ID | Épocas | Clases | Entrenamiento | #Entrenamiento | Test | Precisión | Notas |
|:-:|:-:|:------:|:-------------:|:----:|:----:|:---------:|:-----:|
| 10-02 | 52 |  8     | $T_1(S) + T_2(S)$ | 30 | D | 0.125 | Empezaba con 0.25, pero al poco se redujo |
| 10-03 | 60 | 8 | $S + T_1(S) + T_2(S)$ | 45 | D | 0.25/0.375 | Existe variación, llegando a 0.375 en varias ocasiones |
| 10-04 | 51 | 8 | $S$ | 15 | D | 0.125 | |
| 10-05 | 51 | 8 | $T_1(S)$ | 15 | D | 0.125 | |
| 10-06 | 33 | 8 | $S + DF(S_{1,2})$ | 26 | D | 0.125 | |
| 10-07 | ?? | 8 | $S + T_1(S)$ | 32 | D | 0.25 | Mejoras claras desde el principio |
| 10-08 | 32 | 8 | $S + T_1(DF(S_{1,2}))$ | 26 | D | 0.125 | Nótese que no se considera $T_1(S \setminus S_{1,2})$ |
| 10-09-01 | 22 | 8 | $S + T_1(S) + DF(S_{1,2})$ | 42 | D | 0.125 | Llega a 0.25 y 0.375 al principio |
| 10-09-02 | 25 | 8 | $S + T_1(S) + T_1(DF(S_{1,2}))$ | 42 | D | 0.375 | LLega a 0.25 en 162 pasos, y en 266 a la marca|

> **Nota**: En cada paso se actualizan los pesos y se trabaja con un lote del conjunto de entrenamiento.

## Trabajo relacionado

## Líneas de trabajo futuras

## Líneas de trabajo descartadas
