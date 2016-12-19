# Gestión Productiva 2.2
## Alumno: Marvin Flores
## Profesor: Ing. Priscila Valdiviezo

## Tema:

Crear un sistema de reconocimiento de imágenes y rostros, para su uso en un Salón Inteligente.
Usando la plataforma de Bluemix de IBM Watson:

- Habilitar Ingreso a un laboratorio.
- Cómo Ingreso al Sistema EVA.
- Perfil de un Profesor. etc.


## Modo de Uso:

Bluemix es un entorno desarrollado como una arquitectura de Plataforma como Servicio: PaaS.


![image1](https://lh6.googleusercontent.com/mpL4xY_g82MIrPtqJGJsHzs75Qh-7tJOmCWq7y39UnYU99t2_tqxiFgWbLiXzyainks0uBSt_uDDabBNlZmiAdqGonUeTRL69YSgCrzEEPF_Ily8FwOXkhc-bl-6nNQwOuCQFr0_oKE)

## Ejemplo:

Si quiere reconocer a un personaje famoso:

![image2](https://lh3.googleusercontent.com/0QTJjMr2sQTex8Zn4b5hyRF6WPFlCFWuGucwS6fHk_eZSySfquH0cTK6l3I8vmN6hklejYyuOlv6fQGhKPIswdF77S8FEyf0-6xEuN9Xr4tLjYlm63cmv1Fjg8faJBrGZ3Fb-lcreAk)

    {
      "age": {
      "max": 44,
      "min": 35,
      "score": 0.373973},
      "face_location": {
      "height": 390,
      "left": 71,
      "top": 167,
      "width": 341 },
      "gender": {
      "gender": "FEMALE",
      "score": 0.993307  },
      "identity": {
      "name": "Whoopi Goldberg",
      "score": 0.989013,
      "type_hierarchy": "/people/women/celebrities/whoopi goldberg" } 
    } 


## Como usar la API:
1. Registrarnos en la Plataforma (Free Plan: 30 días)
2. Elegimos del catálogo que Api queremos usar. (Free Plan: Hasta 10)
3. Generar Credenciales de Api:
![image3](https://lh3.googleusercontent.com/dYrW0Dj6-W9m9joccFqOtMBk0jiSJJ98ORSt-2WBvgaccTGEdMZ-niiBvO4LVCyHWrTLeDWU63E1jF9P_KRXjQ916malM_lhIF0RjZcx8YR-M_JTuRD8_a3T3aeNYji4x2XSUwV-AGg)


**Credenciales:**

    {
      "url": "https://gateway-a.watsonplatform.net/visual-recognition/api",
      "note": "It may take up to 5 minutes for this key to become active",
      "api_key": "f9c27480a6049322777c1b034607993bc568781c"
    }
## Ejemplo uso de la Api:
    curl -X POST -F "images_file=@/home/elmarvin/BluemixPruebas/test3.jpg"
    "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/detect_faces?api_key={f9c27480a6049322777c1b034607993bc568781c}&version=2016-05-20";
![image4](https://lh4.googleusercontent.com/GVt4pb-8ErbeNz_tKlNiLF1AMfEZKdSLpvCXOZiMzFUeQZEgy4PWZxJOMYg8vsb3FW6FpqXii3jsTyAUmV5N56HTPrur8YuXQs-f_8KEiu_2unLmzNWDoIQqqBwunoFsouiy_HTW5BI)


**Respuesta:**

    { 
       "images": [ 
           { 
               "faces": [ 
                   { 
                       "age": { 
                           "max": 44, 
                           "min": 35, 
                           "score": 0.389988 
                       }, 
                       "face_location": { 
                           "height": 261, 
                           "left": 128, 
                           "top": 113, 
                           "width": 221 
                       }, 
                       "gender": { 
                           "gender": "MALE", 
                           "score": 0.993307 
                       }, 
                       "identity": { 
                           "name": "Vladimir Putin", 
                           "score": 0.970688, 
                           "type_hierarchy": "/people/world leaders/vladimir putin" 
                       } 
                   } 
               ], 
               "image": "test3.jpg" 
           } 
       ], 
       "images_processed": 1 
    }


## Creando tu Propio Clasificador:

    curl -X POST -F "alexis_positive_examples=@/home/elmarvin/bluemixpruebas/alexis.zip" -F "majo_positive_examples=@/home/elmarvin/bluemixpruebas/mariajose.zip" -F "marvin_positive_examples=@/home/elmarvin/bluemixpruebas/marvin.zip" -F "rosita_positive_examples=@/home/elmarvin/bluemixpruebas/rosita.zip"  -F "name=friends" "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classifiers?api_key={f9c27480a6049322777c1b034607993bc568781c}&version=2016-05-20"
    
    //Respuesta
    { 
       "classifier_id": "friends_580483461", 
       "name": "friends", 
       "owner": "c19cdcbd-8275-40aa-bfbf-a2f443d7c039", 
       "status": "training", 
       "created": "2016-10-30T03:37:13.088Z", 
       "classes": [ 
           {"class": "rosita"}, 
           {"class": "marvin"}, 
           {"class": "majo"}, 
           {"class": "alexis"} 
       ] 
    }

Comprobar Status:

    curl -X GET "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classifiers/{friends_580483461}?api_key={f9c27480a6049322777c1b034607993bc568781c}&version=2016-05-20"
    
    //RESPUESTA:
    { 
       "classifier_id": "friends_580483461", 
       "name": "friends", 
       "owner": "c19cdcbd-8275-40aa-bfbf-a2f443d7c039", 
       "status": "ready", 
       "created": "2016-10-30T03:37:13.088Z", 
       "classes": [ 
           {"class": "rosita"}, 
           {"class": "marvin"}, 
           {"class": "majo"}, 
           {"class": "alexis"} 
       ] 
    }

Resultados pruebas del Clasificador:

    curl -X POST -F "images_file=@/home/elmarvin/bluemixpruebas/alexis11.jpg" -F "parameters=@/home/elmarvin/bluemixpruebas/myparams.json" "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key={f9c27480a6049322777c1b034607993bc568781c}&version=2016-05-20"
    
    RESPUESTA:
    { 
       "custom_classes": 4, 
       "images": [ 
           { 
               "classifiers": [ 
                   { 
                       "classes": [ 
                           { 
                               "class": "person", 
                               "score": 0.890903, 
                               "type_hierarchy": "/people" 
                           } 
                       ], 
                       "classifier_id": "default", 
                       "name": "default" 
                   }, 
                   { 
                       "classes": [ 
                           { 
                               "class": "alexis", 
                               "score": 0.867398 
                               //Marvin: 0.727598
                               //Majo: 0.707891
                               //Rosita: 0.693523
                           } 
                       ], 
                       "classifier_id": "friends_580483461", 
                       "name": "friends" 
                   } 
               ], 
               "image": "alexis11.jpg" 
           } 
       ], 
       "images_processed": 1 
    }

Error en la clasificación:

![image5](https://d2mxuefqeaa7sj.cloudfront.net/s_E93218D914AEFD241EB1B462D33BAA794B02F22FCE5E7C6ECED9BEEAD6B6558D_1482174081338_file.png)

    curl -X POST -F "images_file=@/home/elmarvin/bluemixpruebas/grace.jpg" -F "parameters=@/home/elmarvin/bluemixpruebas/mypar
    ams.json" "https://gateway-a.watsonplatform.net/visual-recognition/api/v3/classify?api_key={f9c27480a6049322777c1b034607993bc568781c}&version=2016-05
    -20"
    
    //RESPUESTA 
    { 
       "custom_classes": 4, 
       "images": [ 
           { 
               "classifiers": [ 
                   { 
                       "classes": [ 
                           { 
                               "class": "person", 
                               "score": 0.999963, 
                               "type_hierarchy": "/people" 
                           } 
                       ], 
                       "classifier_id": "default", 
                       "name": "default" 
                   }, 
                   { 
                       "classes": [ 
                           { 
                               "class": "rosita", 
                               "score": 0.730824 
                           } 
                       ], 
                       "classifier_id": "friends_580483461", 
                       "name": "friends" 
                   } 
               ], 
               "image": "grace.jpg" 
           } 
       ], 
       "images_processed": 1 
    }
