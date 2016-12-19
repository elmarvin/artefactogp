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

# OpenCV

http://opencv.org/platforms/android.html
http://www.genbeta.com/actualidad/openface-un-nuevo-software-de-reconocimiento-facial-de-codigo-abierto
http://robologs.net/2014/05/26/reconocimiento-facial-con-opencv-webcam/
http://josbram.delifrut.cl/files/openCV/tutorial_opencv.pdf (2008)

Lista de Tutoriales OpenCv
http://acodigo.blogspot.com/p/tutorial-opencv.html

**OpenCV** es una [biblioteca](https://es.wikipedia.org/wiki/Biblioteca_(programaci%C3%B3n)) libre de visión artificial originalmente desarrollada por [Intel](https://es.wikipedia.org/wiki/Intel_Corporation).
Open CV es multiplataforma, existiendo versiones para [GNU/Linux](https://es.wikipedia.org/wiki/GNU/Linux), [Mac OS X](https://es.wikipedia.org/wiki/Mac_OS_X) y [Windows](https://es.wikipedia.org/wiki/Microsoft_Windows). Contiene más de 500 funciones que abarcan una gran gama de áreas en el proceso de visión, como reconocimiento de objetos ([reconocimiento facial](https://es.wikipedia.org/w/index.php?title=Reconocimiento_facial&action=edit&redlink=1)), calibración de cámaras, visión estérea y visión robótica.

## **Reconociemiento Facial:
**
En el reconocimiento facial como un proceso de dos fases.

- Fase 1: Detectar la presencia de caras en una imagen o una secuencia de video usando métodos como cascadas de Haar, HOG + SVM lineal, aprendizaje profundo, o cualquier otro algoritmo que pueda localizar las caras.
- Fase 2: Tome cada una de las caras detectadas durante la fase de localización e identifique cada una de ellas - aquí es donde realmente asignamos un nombre auna cara.


## Algoritmos de Reconocimiento Facial:

**Eigenfaces**
El algoritmo de Eigenfaces utiliza el Análisis de Componentes Principales para construir una representación dimensional baja de las imágenes de la cara.
Esto implica recolectar un conjunto de datos de caras con múltiples imágenes de la cara por persona que queremos identificar - como tener múltiples ejemplos de entrenamiento de cada imagen que queremos etiquetar. Dado este conjunto de datos de las imágenes faciales (se supone que tienen el mismo ancho, altura e idealmente - con sus ojos y estructuras faciales alineadas al mismo (x, y), se aplica una descomposición del valor propio del conjunto de datos, manteniendo los autovectores con los valores propios correspondientes más grandes.

**Implementación Java:**


    package reconocimiento;
     
    import com.googlecode.javacv.cpp.opencv_core.CvRect;
    import com.googlecode.javacv.cpp.opencv_core.CvSeq;
    import com.googlecode.javacv.cpp.opencv_core.IplImage;
    import static com.googlecode.javacv.cpp.opencv_core.cvGetSeqElem;
    import static com.googlecode.javacv.cpp.opencv_highgui.cvLoadImage;
    import java.util.logging.Level;
    import java.util.logging.Logger;
     
    public class Main {
        public static void main(String args[]){
            try {
                ReconocimientoCaras reconocer = ReconocimientoCaras.getInstance();
     
                //Entrenamiento
                IplImage[] trainImages = new IplImage[10];
                for(int i=1; i &lt; = 10; i++){
                    trainImages[i-1]=cvLoadImage("terry"+i+".jpg");
                    CvSeq faces = reconocer.detectFace(trainImages[i-1]);
                    CvRect r = new CvRect(cvGetSeqElem(faces,0));
                    trainImages[i-1]=reconocer.preprocessImage(trainImages[i-1], r);
                }
                reconocer.learnNewFace("John Terry", trainImages);
     
                //Reconocimiento
                IplImage target = new IplImage();
                target = cvLoadImage("cr7_target.jpg");
                CvSeq faces2 = reconocer.detectFace(target);
                CvRect r2 = new CvRect(cvGetSeqElem(faces2,0));
                target=reconocer.preprocessImage(target, r2);
                System.out.println("Persona Identificada: "+reconocer.identifyFace(target));
            } catch (Exception ex) {
                Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
            }
     
        }
    }


![imageocv1](https://jonathanmelgoza.com/blog/wp-content/uploads/2013/12/Ejemplo-de-Identificacion-de-Caras-en-Java-con-OpenCV-2-300x246.jpg)


**LBPs for face recognition**
**Patrones Binarios Locales (LBPs)** se basa en la extracción de características.
La imagen se divide en regiones uniformes mediante una grilla cuadricular (bloques 7x7). Luego se calculan los histogramas para cada bloque y se concatenan todos para obtener el patrón de la cara. De esta forma se logra efectivamente una descripción de la cara en 3 niveles diferentes de ubicación: las etiquetas contienen información de los 8 patrones a nivel de los píxeles, los histogramas en una pequeña región producen información a nivel regional y los histogramas regionales son concatenados para crear una descripción global de la cara.
Los histograma obtenidos mediante el procedimiento descrito contiene información acerca de la distribución local de los micropatrones, como bordes, puntos y otros, sobre la imagen completa.

![imageocv2](https://d2mxuefqeaa7sj.cloudfront.net/s_550CDD17EE6EF28948E4B3BF6CD842350A0C9E8B6E22DAF453FCB620E335A985_1482181883739_file.png)



## Implementación Python:
    # USAGE
    # python lbp_faces.py --dataset ~/Desktop/caltech_faces
    
    # import the necessary packages
    from __future__ import print_function
    from pyimagesearch.face_recognition.datasets import load_caltech_faces
    from sklearn.preprocessing import LabelEncoder
    from sklearn.metrics import classification_report
    import numpy as np
    import argparse
    import imutils
    import cv2
    
    # construct the argument parse and parse command line arguments
    ap = argparse.ArgumentParser()
    ap.add_argument("-d", "--dataset", required=True, help="path to CALTECH Faces dataset")
    ap.add_argument("-s", "--sample-size", type=int, default=10, help="# of example samples")
    args = vars(ap.parse_args())
    
    # load the CALTECH faces dataset
    print("[INFO] loading CALTECH Faces dataset...")
    (training, testing, names) = load_caltech_faces(args["dataset"], min_faces=21,
            test_size=0.25)
    
    # encode the labels, transforming them from strings into integers since OpenCV does
    # not like strings as training data
    le = LabelEncoder()
    le.fit_transform(training.target)
    
    # train the Local Binary Pattern face recognizer
    print("[INFO] training face recognizer...")
    recognizer = cv2.createLBPHFaceRecognizer(radius=2, neighbors=16, grid_x=8, grid_y=8)
    recognizer.train(training.data, le.transform(training.target))
    
    # initialize the list of predictions and confidence scores
    print("[INFO] gathering predictions...")
    predictions = []
    confidence = []
    
    # loop over the test data
    for i in xrange(0, len(testing.data)):
            # classify the face and update the list of predictions and confidence scores
            (prediction, conf) = recognizer.predict(testing.data[i])
            predictions.append(prediction)
            confidence.append(conf)
    
    # show the classification report
    print(classification_report(le.transform(testing.target), predictions, target_names=names))
    
    # loop over the the desired number of samples
    for i in np.random.randint(0, high=len(testing.data), size=(args["sample_size"],)):
            # resize the face to make it more visable, then display the face and the prediction
            print("[INFO] Prediction: {}, Actual: {}, Confidence: {:.2f}".format(
                    le.inverse_transform(predictions[i]), testing.target[i], confidence[i]))
            face = testing.data[i]
            face = imutils.resize(face, width=face.shape[1] * 2, inter=cv2.INTER_CUBIC)
            cv2.imshow("Face", face)
            cv2.waitKey(0)

**Ejemplo:**

![imageocv3](https://d2mxuefqeaa7sj.cloudfront.net/s_550CDD17EE6EF28948E4B3BF6CD842350A0C9E8B6E22DAF453FCB620E335A985_1482181842706_file.png)
